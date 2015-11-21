Velvet Assembly
===============

Velvet was one of the first de novo genomic assemblers specially designed for short read sequencing technologies. It was  developed by Daniel Zerbino and Ewan Birney at the European Bioinformatics Institute (EMBL-EBI). Velvet currently takes in short read sequences, removes errors then produces high quality unique contigs. It then uses paired-end read and long read information, when available, to retrieve the repeated areas between contigs. See the `Velvet home page <https://www.ebi.ac.uk/~zerbino/velvet/>`_ for more info.

Step 1: velveth
---------------
``velveth`` takes in a number of sequence files, produces a hashtable, then
outputs two files in an output directory (creating it if necessary), Sequences
and Roadmaps, which are necessary for running ``velvetg`` in the next step.

Let's create multiple hashtables using kmer-lengths of 31 and 51. We are going to 
submit the jobs to the compute cluster using ``qsub``,asking for a machine with
24 cores (``-pe multislot 24``). You can check the status of your job using the
command ``qstat``::

  cd ~/workdir/assembly/
  
  qsub -cwd -pe multislot 24 -N velveth_31  -l mtc=1 -b y \ 
  /vol/cmg/bin/velveth velvet_31 31 -shortPaired -fastq -separate read1.fq read2.fq
  
  qsub -cwd -pe multislot 24 -N velveth_51  -l mtc=1 -b y \ 
  /vol/cmg/bin/velveth velvet_51 51 -shortPaired -fastq -separate read1.fq read2.fq

Note: You can check the status of your job using the command ``qstat``::

  >>>statler:~/workdir/assembly>qstat
  job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
  -----------------------------------------------------------------------------------------------------------------
  3888958 0.65000 velveth_31 asczyrba     r     11/21/2015 07:18:29 all.q@suc01016.CeBiTec.Uni-Bie    24        
  3888959 0.45213 velveth_51 asczyrba     r     11/21/2015 07:18:45 all.q@suc01003.CeBiTec.Uni-Bie    24        

If you do not see your jobs using ``qstat`` anymore, they are finished.
You should have two output directories for the two different kmer-lengths: `velvet_31` and `velvet_51`.

Step 2: velvetg
---------------
Now we have to start the actual assembly using ``velvetg``. ``velvetg`` is the core of Velvet where the de Bruijn graph is built then manipulated. Let's run assemblies for both kmer-lengths. See the `Velvet manual <https://www.ebi.ac.uk/~zerbino/velvet/Manual.pdf>`_ for more info about parameter settings. Again, we submit the job to the compute cluster::

  qsub -cwd -pe multislot 24 -N velvetg_31  -l mtc=1 -b y \ 
  /vol/cmg/bin/velvetg velvet_31 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto
  
  qsub -cwd -pe multislot 24 -N velvetg_51  -l mtc=1 -b y \ 
  /vol/cmg/bin/velvetg velvet_51 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto 

The contig sequences are located in the `velvet_31` and `velvet_51` directories in file `contigs.fa`. Let's get some very basic statistics on the contigs. The script ``getN50.pl`` reads the contig file and computes the total length of the assembly, number of contigs, N50 and largest contig size. In our example we will exclude contigs shorter than 500bp (option `-s 500`)::

  getN50.pl -s 500 -f velvet_31/contigs.fa
  getN50.pl -s 500 -f velvet_51/contigs.fa
  
.. include:: note_top.rst
