IDBA-UD Assembly
================

IDBA is the basic iterative de Bruijn graph assembler for
second-generation sequencing reads. IDBA-UD, an extension of IDBA, is
designed to utilize paired-end reads to assemble low-depth regions and
use progressive depth on contigs to reduce errors in high-depth
regions. It is a generic purpose assembler and epspacially good for
single-cell and metagenomic sequencing data. See the `IDBA home page
<https://github.com/loneknightpy/idba>`_ for more info.

IDBA-UD requires paired-end reads stored in single FastA file and a
pair of reads is in consecutive two lines. You can use `fq2fa` (part
of the IDBA repository) to merge two FastQ read files to a single
file. The following command will generate a FASTA formatted file
called `reads12.fas` by "shuffling" the reads from FASTQ files
`read1.fq` and `read2.fq`::


  cd /mnt/volume/workdir/assembly/

  fq2fa --merge read1.fq read2.fq reads12.fas
  
IDBA-UD can be run by the following command. As our compute instances
have multiple cores, we use the option `--num_threads 14` to tell
IDBA-UD it should use 14 parallel threads::

  cd /mnt/volume/workdir/assembly/

  idba_ud -r reads12.fas --num_threads 14 -o idba_ud_out

The contig sequences are located in the `idba_ud_out` directory in file `contig.fa`. Again, let's get some  basic statistics on the contigs::

  getN50.pl -s 500 -f idba_ud_out/contig.fa

