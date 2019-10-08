The Tutorial Data Set
================================

We have prepared a small toy data set for this tutorial. The data is
already located on the SimpleVM instance in the
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

Create a working directory in the additional storage volume which you
configured when you started the SimpleVM and copy the data to the
working directory::

  sudo chown ubuntu:ubuntu /mnt/volume
  mkdir -p /mnt/volume/workdir/assembly
  cd /mnt/volume/workdir/assembly
  cp -rv ~/WGS-data/* .

Next, we will activate the bioconda virtual environment, which
includes all installed software tools::

  source ~/miniconda3/bin/activate denbi



