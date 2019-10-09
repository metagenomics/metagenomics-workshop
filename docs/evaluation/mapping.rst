Read Mapping
============

In this part of the tutorial we will look at the assemblies by mapping
the reads to the assembled contigs.  Different tools exists for
mapping reads to genomic sequences such as `bowtie
<http://bowtie-bio.sourceforge.net/bowtie2/index.shtml>`_ or `bwa
<http://bio-bwa.sourceforge.net/>`_. Today, we will use the tool
BBMap.

BBMap: Short read aligner for DNA and RNA-seq data. Capable of
handling arbitrarily large genomes with millions of scaffolds. Handles
Illumina, PacBio, 454, and other reads; very high sensitivity and
tolerant of errors and numerous large indels. Very fast. See the
`BBTools home page <https://jgi.doe.gov/data-and-tools/bbtools/bb-tools-user-guide/>`_ for more
info.


``bbmap`` needs to build an index for the contigs sequences before it
can map the reads onto them. Here is an example command line for
mapping the reads back to the MEGAHIT assembly::

  cd /mnt/volume/workdir/assembly/megahit_out

  bbmap.sh ref=final.contigs.fa
  
Now that we have an index, we can map the reads::

  bbmap.sh in=../read1.fq in2=../read2.fq out=megahit.bam threads=14
  
``bbmap`` produces output in BAM format (the binary version of the `SAM format
<http://samtools.github.io/hts-specs/SAMv1.pdf>`_). BAM files can be viewed and manipulated with `SAMtools <http://www.htslib.org/>`_. Let's first build an index for the FASTA file::

  samtools faidx final.contigs.fa

We have to sort the BAM file by starting position of the alignments. This can be done using samtools again::

  samtools sort -o megahit_sorted.bam -@ 14 megahit.bam 
  
Now we have to index the sorted BAM file::

  samtools index megahit_sorted.bam
  
To look at the BAM file use::

  samtools view megahit_sorted.bam | less
  
We will use the IGV genome browser to look at the mappings::

  ~/IGV_Linux_2.7.0/igv.sh
  
Now let's look at the mapped reads:

1. Load the contig sequences into IGV. Use the menu ``Genomes->Load Genome from File...`` 
2. Load the BAM file into IGV. Use menu ``File->Load from File...`` 
3. Load the predicted genes as another track. Use menu ``File->Load from File...`` to load the GFF file.


