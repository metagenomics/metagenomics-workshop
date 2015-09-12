Read Mapping
============

In this part of the tutorial we will look at the assemblies by mapping the reads to the assembled contigs.
Different tools exists for mapping reads to genomic sequences such as `bowtie <http://bowtie-bio.sourceforge.net/bowtie2/index.shtml>`_ or `bwa <http://bio-bwa.sourceforge.net/>`_. Today, we will use the tool BBMap.

BBMap: Short read aligner for DNA and RNA-seq data. Capable of handling arbitrarily large genomes with millions of scaffolds. Handles Illumina, PacBio, 454, and other reads; very high sensitivity and tolerant of errors and numerous large indels. Very fast. See the `BBMap home page <http://sourceforge.net/projects/bbmap/>`_ for more info.


``bbmap`` needs to build an index for the contigs sequences before it can map the reads onto them. Here is an example command line for mapping the reads back to the MEGAHIT assembly::

  cd /vol/spool/tutorial-data/megahit_out
  ~/bbmap/bbmap.sh ref=final.contigs.fa
  
Now that we have an index, we can map the reads. 

  ~/bbmap/bbmap.sh in=../read1.fq in2=../read2.fq out=megahit.sam bamscript=sam2bam.sh
  
The output is in SAM format, usually you want to convert this into a sorted BAM file. ``bbamp`` creates a shell script which can be used to convert ``bbmap``'s output into BAM format::

  source sam2bam.sh
  

