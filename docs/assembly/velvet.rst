Velvet Assembly
===============

Velvet was one of the first de novo genomic assemblers specially designed for short read sequencing technologies. It was  developed by Daniel Zerbino and Ewan Birney at the European Bioinformatics Institute (EMBL-EBI). Velvet currently takes in short read sequences, removes errors then produces high quality unique contigs. It then uses paired-end read and long read information, when available, to retrieve the repeated areas between contigs. See the `Velvet home page <https://www.ebi.ac.uk/~zerbino/velvet/>`_ for more info.

Step 1: velveth
---------------
``velveth`` takes in a number of sequence files, produces a hashtable, then
outputs two files in an output directory (creating it if necessary), Sequences
and Roadmaps, which are necessary for running ``velvetg`` in the next step.

Let's create multiple hashtables using kmer-lengths of 31 and 51. We are going to redirect the output into a file `velveth_31.log` and `velveth_51.log`::

  velveth velvet_31 31 -shortPaired -fastq -separate read1.fq read2.fq >& velveth_31.log &
  velveth velvet_51 51 -shortPaired -fastq -separate read1.fq read2.fq >& velveth_51.log &

This will create two output directories for the two different kmer-lengths: `velvet_31` and `velvet_51`.

Step 2: velvetg
---------------
Now we have to start the actual assembly using ``velvetg``. ``velvetg`` is the core of Velvet where the de Bruijn graph is built then manipulated. Let's run assemblies for both kmer-lengths. See the `Velvet manual <https://www.ebi.ac.uk/~zerbino/velvet/Manual.pdf>`_ for more info about parameter settings. Again, output will be redirected to log-files `velvetg_31.log` and `velvetg_51.log`::

  velvetg velvet_31 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto >& velvetg_31.log &
  velvetg velvet_51 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto >& velvetg_51.log &

The contig sequences are located in the `velvet_31` and `velvet_51` directories in file `contigs.fa`. Let's get some very basic statistics on the contigs. The script ``getN50.pl`` reads the contig file and computes the total length of the assembly, number of contigs, N50 and largest contig size. In our example we will exclude contigs shorter than 500bp (option `-s 500`)::

  getN50.pl -s 500 -f velvet_31/contigs.fa
  getN50.pl -s 500 -f velvet_51/contigs.fa
  
.. note:: Most jobs above will be started in the backgroud using the ``&`` at the end of each command, 
          which allows you to continue working in the shell. You can watch your running jobs by typing ``top`` 
          (hit ``q`` to exit ``top``). You can look into the log-files by typing e.g. ``less velvetg_31.log``.


