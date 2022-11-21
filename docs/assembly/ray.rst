Ray Assembly
============

Ray is a parallel software that computes de novo genome assemblies
with next-generation sequencing data.  Ray is written in C++ and can
run in parallel on numerous interconnected computers using the
message-passing interface (MPI) standard. See the `Ray home page
<http://denovoassembler.sourceforge.net/>`_ for more info.

Ray can be run by the following command using a kmer-length of 51 and
31, repectively. As our compute instance have multiple cores, we
specify this in the `mpiexec -n 28 ` command to let Ray know it should
use 28 parallel MPI processes::

  cd /mnt/WGS-data

  mpiexec -n 28 /usr/local/bin/Ray -k 51 -p read1.fq read2.fq -o ray_51

If there is enough time, you can run another Ray assembly using a smaller
kmer size::

  mpiexec -n 28 /usr/local/bin/Ray -k 31 -p read1.fq read2.fq -o ray_31

This will create the output directory `ray_51` (and `ray_31`), the final
contigs are located in `ray_51/Contigs.fasta` (and
`ray_31/Contigs.fasta`).  Again, let's get some basic statistics on the
contigs::

  getN50.pl -s 500 -f ray_51/Contigs.fasta
  getN50.pl -s 500 -f ray_31/Contigs.fasta

Now that you have run assemblies using Velvet, MEGAHIT, IDBA-UD and Ray, let's have a quick look at the assembly statistics of all of them::

  cd /mnt/WGS-data
  sh ./get_assembly_stats.sh
  
