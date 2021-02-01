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

  cd /mnt/WGS-data/megahit_out
  mkdir metabat
  cd metabat
  
  runMetaBat.sh ../final.contigs.fa ../megahit_sorted.bam
  
MetaBAT will generate 11 bins from our assembly::

  ls final.contigs.fa.metabat-bins
  
  bin.1.fa
  bin.2.fa
  bin.3.fa
  bin.4.fa
  bin.5.fa
  bin.6.fa
  bin.7.fa
  bin.8.fa
  bin.9.fa
  bin.10.fa
  bin.11.fa
