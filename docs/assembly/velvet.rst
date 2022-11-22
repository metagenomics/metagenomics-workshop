Velvet Assembly
===============

Velvet was one of the first de novo genomic assemblers specially
designed for short read sequencing technologies. It was developed by
Daniel Zerbino and Ewan Birney at the European Bioinformatics
Institute (EMBL-EBI). Velvet currently takes in short read sequences,
removes errors then produces high quality unique contigs. It then uses
paired-end read and long read information, when available, to retrieve
the repeated areas between contigs. See the `Velvet GitHub page
<https://github.com/dzerbino/velvet>`_ for more info.

Step 1: velveth
---------------
``velveth`` takes in a number of sequence files, produces a hashtable, then
outputs two files in an output directory (creating it if necessary), Sequences
and Roadmaps, which are necessary for running ``velvetg`` in the next step.

Let's create multiple hashtables using kmer-lengths of 31 and 51. We
are going to run two jobs in parallel::

  cd /mnt/WGS-data
  
  velveth velvet_31 31 -shortPaired -fastq -separate read1.fq read2.fq &
  velveth velvet_51 51 -shortPaired -fastq -separate read1.fq read2.fq &

Once the two jobs are finished (use `top` to monitor your jobs), you 
should have two output directories for the two different kmer-lengths: 
`velvet_31` and `velvet_51`.

Step 2: velvetg
---------------

Now we have to start the actual assembly using
``velvetg``. ``velvetg`` is the core of Velvet where the de Bruijn
graph is built then manipulated. Let's run assemblies for both
kmer-lengths. See the `Velvet manual
<https://github.com/dzerbino/velvet/blob/master/Manual.pdf>`_ for more
info about parameter settings. Run::

  velvetg velvet_31 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto &
  velvetg velvet_51 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto &

The contig sequences are located in the `velvet_31` and `velvet_51`
directories in file `contigs.fa`. Let's get some very basic statistics
on the contigs. The script ``getN50.pl`` reads the contig file and
computes the total length of the assembly, number of contigs, N50 and
largest contig size. In our example we will exclude contigs shorter
than 500bp (option `-s 500`)::

  getN50.pl -s 500 -f velvet_31/contigs.fa
  getN50.pl -s 500 -f velvet_51/contigs.fa
  
