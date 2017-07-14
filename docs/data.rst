The Tutorial Data Set
================================

Note: This tutorial was prepared for a training workshop utilizing
our local compute infrastrucutre. If you want to download the data set
to your machine and run it locally, you can find the data 
`here <https://uni-bielefeld.sciebo.de/index.php/s/FpiLaNWWp5MDVui>`_.

We have prepared a small toy data set for this tutorial. The data is located 
in `/vol/metagencourse/DATA/WGS-data` directory, which has the following content:

+---------------+--------------------------------------------+
| File          | Content                                    |
+===============+============================================+
| genomes/      | Directory containing the reference genomes |
+---------------+--------------------------------------------+
| gold_std/     | Gold Standard assemblies                   |
+---------------+--------------------------------------------+
| read1.fq      | Read 1 of paired reads (FASTQ)             |
+---------------+--------------------------------------------+
| read2.fq      | Read 2 of paired reads (FASTQ)             |
+---------------+--------------------------------------------+
| reads.fas     | Shuffled reads (FASTA)                     |
+---------------+--------------------------------------------+

Create a working directory in your home directory and symbolic links
to the data files::

  cd ~/workdir
  mkdir assembly
  cd assembly
  ln -s /vol/metagencourse/DATA/WGS-data/* .


