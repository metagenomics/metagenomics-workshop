Ray Assembly
============

Ray is a parallel software that computes de novo genome assemblies
with next-generation sequencing data.  Ray is written in C++ and can
run in parallel on numerous interconnected computers using the
message-passing interface (MPI) standard. See the `Ray home page
<http://denovoassembler.sourceforge.net/>`_ for more info.

Ray can be run by the following command using a kmer-length of 31. As
our compute instance have multiple cores, we specify this in the
`mpiexec -n 12 ` command to let Ray know it should use 12 parallel MPI
processes::

  cd ~/workdir/assembly/

  qsub -cwd -pe multislot 12 -N ray -b y \
  /usr/bin/mpiexec -n 12 /usr/bin/Ray -k 31 -p read1.fq read2.fq -o ray_31

This will create the output directory `ray_31` and the final contigs are located in `ray_31/Contigs.fasta`.
Again, let's get some basic statistics on the contigs::

  getN50.pl -s 500 -f ray_31/Contigs.fasta

Now that you have run assemblies using Velvet, MEGAHIT, IDBA-UD and Ray, let's have a quick look at the assembly statistics of all of them::

  cd ~/workdir/assembly/
  ./get_assembly_stats.sh
  
.. include:: note_top.rst
