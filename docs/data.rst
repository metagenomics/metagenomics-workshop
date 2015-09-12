Download the Tutorial Data Set
================================

We have prepared a small toy data set for this tutorial. You can download
the data set using the following commands::

  cd /vol/spool
  java -jar ~/bibis3-1.6.0.jar -d --region eu-west-1 s3://mg-tutorial/tutorial-data.tar .

Unzip the tar-ball and change to the data directory::

  tar xf tutorial-data.tar
  cd tutorial-data

The `tutorial-data` directory includes the following files:

====      =======
File      Content
====      =======
read1.fq  Read 1 of read pair (FASTQ format)
read2.fq  Read 2 of read pair (FASTQ format)
reads.fas Shuffled read (FASTA format)
=====     ======

