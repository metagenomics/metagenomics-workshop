The Tutorial Data Set
================================

We have prepared a small toy data set for this tutorial. Please use the
following commands to download the data to your VM::

  sudo chown ubuntu:ubuntu /mnt
  cd /mnt
  wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/denbi-mg-course/WGS-data.tar
  tar xvf WGS-data.tar
  cd ~
  ln -s /mnt/WGS-data .
  
The `~/WGS-data` directory, which has the following content:

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

