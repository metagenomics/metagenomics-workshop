metaSPAdes Assembly
===================

SPAdes – St. Petersburg genome assembler – is an assembly toolkit
containing various assembly pipelines. See the `SPAdes home page
<http://cab.spbu.ru/software/spades/>`_ for more info.

metaSPAdes can be run by the following command::

  cd /mnt/volume/workdir/assembly/

  metaspades.py -o metaspades_out --pe1-1 read1.fq --pe1-2 read2.fq

The contig sequences are located in the `metaspades_out` directory in
file `contigs.fasta`. Again, let's get some basic statistics on the
contigs::

  getN50.pl -s 500 -f metaspades_out/contigs.fasta

