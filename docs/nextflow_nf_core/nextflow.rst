Nextflow
~~~~~~~~~~~

Some of the examples below are from: https://carpentries-incubator.github.io/workflows-nextflow. Please activate the conda env ``nf_metag`` before running any code.

.. code-block:: shell

   conda activate nf_metag
   cd /mnt

Nextflow/Groovy Language Basics
<<<<<<<<<<<<

This guide provides an overview of the basic elements of the Nextflow language.

- **Printing**

In Nextflow, you can print messages to the console using the ``println`` statement.
Please create and open a file named ``ch0.nf`` in the ``/mnt`` directory and write the following code in it

.. code-block:: groovy

   println("Hello, Nextflow!")

Save the file and run it with: ``nextflow run ch0.nf``

- **Methods**

Methods in Nextflow are defined using the Groovy syntax. Here's a simple method definition:

.. code-block:: groovy

   def greet(name) {
       return "Hello, ${name}!"
   }

   println(greet("Nextflow"))

Replace the content of file ``ch0.nf`` with above code save and run it.

- **Comments**

Comments in Nextflow are identical to Groovy/Java:

- Single-line comments start with ``//``.
- Multi-line comments are wrapped in ``/* ... */``.

.. code-block:: groovy

   // This is a single-line comment
   /* This is a
      multi-line comment */

- **Variables**

Variables are declared using the ``def`` keyword or directly with an assignment.

.. code-block:: groovy

   def age = 25
   name = "Nextflow"

- **Data Types**

Nextflow supports various data types, including integers, floats, strings, and booleans.

.. code-block:: groovy

   def age = 25  // Integer
   def pi = 3.14  // Float
   def isActive = true  // Boolean

- **Strings**

Strings can be declared using double quotes ``"``. String interpolation is supported with ``${}``.

.. code-block:: groovy

   def name = "Nextflow"
   println("Hello, ${name}!")

- **Lists**

Lists in Nextflow can be defined using square brackets ``[]``.

.. code-block:: groovy

   def tools = ["Nextflow", "Docker", "Singularity"]
   println(tools[0])  // Prints "Nextflow"

- **Maps**

Maps are key-value pairs and can be defined using the syntax ``[:]``.

.. code-block:: groovy

   def config = [memory: "10 GB", cpus: 4]
   println(config.memory)  // Prints "10 GB"

- **Closures**

Closures are code blocks that can be assigned to variables or passed as arguments.

.. code-block:: groovy

  square = { it * it }
  println(square(3))


Processes
----------
The basic structure of a process is::

  process < NAME > {
    [ directives ]        
    input:                
    < process inputs >
    output:               
    < process outputs >
    when:                 
    < condition >
    [script|shell|exec]:  
    < user script to be executed >
  }

Please create a file named ``ch1.nf`` and write the following code in it:

.. code-block:: groovy

   // nextflow.config file to specify using DSL2
   nextflow.enable.dsl=2
  
   // Define a process
   process seqStats {
      output:
      stdout
      
      """
      seqkit stats /mnt/WGS-data/read1.fq
      """
   }

  // Define a workflow that calls the process
   workflow {
      seqStats().view()
   }


Channels
-----------
There are different types of channels in nextflow:

1. **Value channel**

  A value channel is bound to a single value and can be created with ``Channel.value`` factory method.

2. **Queue channel**

 Queue (consumable) channels can be created using the following channel factory methods.

- ``Channel.of``
- ``Channel.fromList``
- ``Channel.fromPath``
- ``Channel.fromFilePairs``
- ``Channel.fromSRA``

.. code-block:: groovy

  bases = ['A', 'C', 'G', 'T']

  b0_ch = Channel.value(bases)
  b0_ch.view()
  
  b1_ch = Channel.of('A', 'C', 'G', 'T')
  b1_ch.view()
  
  b2_ch = Channel.fromList(bases)
  b2_ch.view()
  
  read1_ch = Channel.fromPath("${projectDir}/WGS-data/*.fq")
  read1_ch.view()
  
  read_pairs_ch = Channel.fromFilePairs("${projectDir}/WGS-data/*{1,2}.fq")
  read_pairs_ch.view()
  
  
  sra_ch = Channel.fromSRA('SRP043510')
  sra_ch.view()

Write the above code in ``ch2.nf``, and run it.

Workflows
----------

We can connect different processes with channels to make a complete workflow. We have already seen a minimal example of workflow in **Processes** section with only one process. We can create a workflow consists of two process in ``ch3.nf``:

.. code-block:: groovy
   
   #!/usr/bin/env nextflow
   
   // nextflow.config file to specify using DSL2
   nextflow.enable.dsl=2
   
   // Define parameters
   params.reads = "/mnt/WGS-data/read{1,2}.fq" // Default pattern for paired-end reads
   params.outdir = "./output_nf" // Default output directory
   params.threads = 8
   
   // QC the reads
   process seqQC {
      tag "${sample_id}"
      
      // Define output dir
      publishDir params.outdir
      // Input file
      input:
      tuple val(sample_id), path(reads)
      
      // Output file
      output:
      tuple val(sample_id), path("*.fastp.{1,2}.fq.gz")
   	
      script:
      def (r1, r2) = reads
   	"""
   	fastp -i $r1 -I $r2 \
           -o ${sample_id}.fastp.1.fq.gz -O ${sample_id}.fastp.2.fq.gz \
           -5 -3 -q 20 --cut_mean_quality 20 -l 80 -w ${params.threads}
   	"""
   }

   // Stats on the QCed reads
   process seqStats {
      tag "${sample_id}"
      publishDir params.outdir, mode: 'move'
      
      input:
      tuple val(sample_id), path(reads)
      
      output:
      tuple val(sample_id), path("*.fastp.stats.txt")
      
      script:
      def seqstats_out = "${sample_id}.fastp.stats.txt"
      """
      seqkit stats -T -a $reads -o $seqstats_out -j $params.threads
      """
   
   }
   
   // Define a workflow that calls the process
   workflow {
       // Create a channel for paired-end input files
       read_pairs_ch = Channel
         .fromFilePairs(params.reads, size: 2, checkIfExists: true)
       seqQC(read_pairs_ch)
       seqStats(seqQC.out)
   }


After the workflow excuted, we should be able to find the final stats output file. We can view it with: 

``csvtk pretty -t output_nf/read.fastp.stats.txt``


Operators
----------

Nextflow provides a powerful set of operators that allow manipulation and control of the data flow. These operators can be categorized into several types based on their functionality: filtering, transforming, splitting, combining, forking, and performing arithmetic operations. This document outlines examples of each category. You can try different operators in ``ch4.nf`` file.

- **Filtering**

The filter operator allows you to get only the items emitted by a channel that satisfy a condition and discarding all the others. 

.. code-block:: groovy

   Channel
    .of( 'a', 'b', 'aa', 'bc', 3, 4.5 )
    .filter( ~/^a.*/ )
    .view()

- **Transforming**

Transforming operators modify the value or data contained in the channel elements. The 

.. code-block:: groovy

   // Example: Transform filenames to uppercase
   Channel
    .fromPath('WGS-data/*.fq')
    .map { file -> file.name.toUpperCase() }
    .view { "Transformed filename: $it" }

   // Converting a list into multiple items
   Channel
    .of([1, 2, 3, 4])
    .flatten()
    .view()
   
   // The reverse of the flatten operator is collect. 
   // The collect operator collects all the items emitted by a 
   //channel to a list and return the resulting object as a sole emission. 
   Channel
    .of( 1, 2, 3, 4 )
    .collect()
    .view()
   
   // Grouping contents of a channel by a key. 
   // The first element of tuple is the default key.
   Channel.fromPath('output_nf/*.fastp.{1,2}.fq.gz')
     .map{file -> [file.name.split('\\.')[0], file]}
     .groupTuple()
     .view()

- **Splitting**

Sometimes, it's necessary to split the content of an individual item in a channel, such as a file or string, into smaller chunks for downstream processing. This could include items stored in a CSV file, entries in FASTA or FASTQ formats, or multi-line strings/text files.

Nextflow provides several splitting operators to facilitate this: ``splitCsv``, ``splitFasta``, ``splitFastq``, ``splitText``

Each of these operators enables precise control over the handling and preprocessing of data streams, enhancing the flexibility and efficiency of Nextflow pipelines.

.. code-block:: groovy

   Channel.of("val1\tval2\tval3\nval4\tval5\tval6\n")
    .splitCsv(sep: "\t")
    .view()

- **Combining**

Combining operators are used to join two or more channels: ``mix``, ``join``

.. code-block:: groovy

  // Example: Combine three channels
  ch1 = Channel.of( 1,2,3 )
  ch2 = Channel.of( 'X','Y' )
  ch3 = Channel.of( 'mt' )
  
  ch4 = ch1.mix(ch2,ch3).view()

  // Joins together the items emitted by two channels for which exists a matching key. 
  // The key is defined, by default, as the first element in each item emitted
  reads1_ch = Channel
    .of(['wt', 'wt_1.fq'], ['mut','mut_1.fq'])
  reads2_ch= Channel
    .of(['wt', 'wt_2.fq'], ['mut','mut_2.fq'])
  reads_ch = reads1_ch
    .join(reads2_ch)
    .view()

- **Forking**

Forking operators split a single channel into multiple channels.

.. code-block:: groovy

  Channel
    .of( 'chr1', 'chr2', 'chr3' )
    .into({ ch1; ch2 })
  
  ch1.view({"ch1 emits: $it"})
  ch2.view({"ch2 emits: $it"})


- **Maths**
The maths operators allows you to apply simple math function on channels.

The maths operators are: ``count``, ``min``, ``max``, ``sum``, ``toInteger``

.. code-block:: groovy

  ch = Channel
   .of(1..22,'X','Y')
   .count()
   .view()


nf-core workflows for metagenomics
----------

- List the nf-core workflows in a specified catagory and sort by stars 
.. code-block:: shell

   nf-core list metagenomics -s stars


+----------------+-------+----------------+--------------+-------------+----------------------+
| Pipeline Name  | Stars | Latest Release | Released     | Last Pulled | Have latest release? |
+================+=======+================+==============+=============+======================+
| mag            | 167   | 2.5.2          | 2 days ago   | 2 days ago  | No (v2.5.1)          |
+----------------+-------+----------------+--------------+-------------+----------------------+
| ampliseq       | 146   | 2.8.0          | 3 weeks ago  | -           | -                    |
+----------------+-------+----------------+--------------+-------------+----------------------+
| eager          | 117   | 2.5.0          | 3 months ago | -           | -                    |
+----------------+-------+----------------+--------------+-------------+----------------------+
| viralrecon     | 105   | 2.6.0          | 11 months ago| -           | -                    |
+----------------+-------+----------------+--------------+-------------+----------------------+
| taxprofiler    | 79    | 1.1.4          | 1 week ago   | 2 days ago  | No (v1.1.4)          |
+----------------+-------+----------------+--------------+-------------+----------------------+
| funcscan       | 49    | 1.1.4          | 3 months ago | -           | -                    |
+----------------+-------+----------------+--------------+-------------+----------------------+


