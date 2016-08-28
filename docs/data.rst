The Tutorial Data Set
================================

From here on, make sure you are actually working on the OpenStack
cloud instance (logged in via ssh) and not on your local workstation
(see previous chapter).

We have prepared a small toy data set for this tutorial. The data is
already located on the OpenStack instance in the
`~/WGS-data` directory, which has the following content:

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

  mkdir -p ~/workdir/assembly
  cd ~/workdir/assembly
  ln -s ~/WGS-data/* .

