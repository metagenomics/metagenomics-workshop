MaxBin Binning
===============

MaxBin is a software that is capable of clustering metagenomic contigs
into different bins, each consists of contigs from one species. MaxBin
uses the nucleotide composition information and contig abundance
information to do achieve binning through an Expectation-Maximization
algorithm. For users' convenience MaxBin will report genome-related
statistics, including estimated completeness, GC content and genome
size in the binning summary page. See the `MaxBin home page
<http://downloads.jbei.org/data/microbial_communities/MaxBin/MaxBin.html>`_
for more info.

Let's run a MaxBin binning on the MEGAHIT assembly. First, we need to
generate an abundance file from the mappes reads::

  cd /mnt/WGS-data/megahit_out
  mkdir maxbin
  cd maxbin
 

Then::

  pileup.sh in=../megahit_sorted.bam  out=cov.txt
  awk '{print $1"\t"$5}' cov.txt | grep -v '^#' > abundance.txt

Activate conda environment for MaxBin::

  conda activate maxbin2

Next, we can run MaxBin::

  run_MaxBin.pl -thread 28 -contig ../final.contigs.fa -out maxbin -abund abundance.txt
  
Assume your output file prefix is (out). MaxBin will generate information using this file header as follows.

+------------------+-------------------------------------------------------------+
| (out).0XX.fasta  | the XX bin. XX are numbers, e.g. out.001.fasta              |
+------------------+-------------------------------------------------------------+
| (out).summary    | summary file describing which contigs are being             |
|                  | classified into which bin.                                  |
+------------------+-------------------------------------------------------------+
| (out).log        | log file recording the core steps of MaxBin algorithm       |
+------------------+-------------------------------------------------------------+
| (out).marker     | marker gene presence numbers for each bin. This table       |
|                  | is ready to be plotted by R or other 3rd-party software.    |
+------------------+-------------------------------------------------------------+
| (out).marker.pdf | visualization of the marker gene presence numbers using R   |
+------------------+-------------------------------------------------------------+
| (out).noclass    | all sequences that pass the minimum length threshold but    |
|                  | are not classified successfully.                            |
+------------------+-------------------------------------------------------------+
| (out).tooshort   | all sequences that do not meet the minimum length threshold.|
+------------------+-------------------------------------------------------------+

Now you can run a gene prediction on each genome bin and BLAST one sequence for each bin
for a (very crude!) classification::

  for i in max*fasta; do prodigal -p meta -a $i.genes.faa -d $i.genes.fna -f gff -o $i.genes.gff -i $i& done

Does the abundance of the bins match the 16S profile of the community?

Lastly, deactivate the conda environment::

  conda deactivate
