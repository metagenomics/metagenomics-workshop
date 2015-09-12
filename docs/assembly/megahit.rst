MEGAHIT Assembly
================

MEGAHIT is a single node assembler for large and complex metagenomics NGS reads, such as soil. It makes use of succinct de Bruijn graph (SdBG) to achieve low memory assembly. MEGAHIT can optionally utilize a CUDA-enabled GPU to accelerate its SdBG contstruction. See the `MEGAHIT home page <https://github.com/voutcn/megahit/>`_ for more info.

MEGAHIT can be run by the following command. As our AWS instance has 16 cores, we use the option `-t 16` to tell MEGAHIT it should use 16 parallel threads. The output will be redirected to file `megahit.log`::

  cd /vol/spool/tutorial-data
  megahit -1 read1.fq -2 read2.fq -t 16 -o megahit_out >& megahit.log &

The contig sequences are located in the `megahit_out` directory in file `final.contigs.fa`. Again, let's get some  basic statistics on the contigs::

  getN50.pl -s 500 -f megahit_out/final.contigs.fa

.. include:: note_top.rst
