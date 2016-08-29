MetaBAT Binning
===============

MetaBAT, An Efficient Tool for Accurately Reconstructing Single
Genomes from Complex Microbial Communities.

Grouping large genomic fragments assembled from shotgun metagenomic
sequences to deconvolute complex microbial communities, or metagenome
binning, enables the study of individual organisms and their
interactions. MetaBAT is an automated metagenome binning software
which integrates empirical probabilistic distances of genome abundance
and tetranucleotide frequency. See the `MetaBAT home page
<https://bitbucket.org/berkeleylab/metabat>`_
for more info.

Let's run a MetaBAT binning on the MEGAHIT assembly::

  cd /vol/spool/workdir/assembly/megahit_out
  mkdir metabat
  cd metabat
  
  qsub -cwd -pe multislot 12 -N metabat -b y \
  /usr/local/bin/runMetaBat.sh ../final.contigs.fa ../megahit_sorted.bam
  
MetaBAT will generate 11 bins from our assembly::

  final.contigs.fa.metabat-bins-.1.fa
  final.contigs.fa.metabat-bins-.2.fa
  final.contigs.fa.metabat-bins-.3.fa
  final.contigs.fa.metabat-bins-.4.fa
  final.contigs.fa.metabat-bins-.5.fa
  final.contigs.fa.metabat-bins-.6.fa
  final.contigs.fa.metabat-bins-.7.fa
  final.contigs.fa.metabat-bins-.8.fa
  final.contigs.fa.metabat-bins-.9.fa
  final.contigs.fa.metabat-bins-.10.fa
  final.contigs.fa.metabat-bins-.11.fa


