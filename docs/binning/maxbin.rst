MaxBin Binning
===============

MaxBin is a software for binning assembled metagenomic sequences based
on an Expectation-Maximization algorithm. For users' convenience
MaxBin will report genome-related statistics, including estimated
completeness, GC content and genome size in the binning summary
page. See the `MaxBin home page
<http://downloads.jbei.org/data/microbial_communities/MaxBin/MaxBin.html>`_ for more info.

Let's run a MaxBin binning on the MEGAHIT assembly. First, we need to generate an
abundance file from the mappes reads::

  ~/bbmap/pileup.sh in=megahit.sam  out=cov.txt
  awk '{print $1,$5}' cov.txt | grep -v '^#' > abundance.txt
  
Next, we can run MaxBin::

  ~/MaxBin-2.1/run_MaxBin.pl -thread 16 -contig final.contigs.fa -out maxbin -abund abundance.txt
  

