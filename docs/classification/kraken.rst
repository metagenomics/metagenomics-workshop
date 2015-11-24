Kraken Taxonomic Sequence Classification System
===============

Kraken is a system for assigning taxonomic labels to short DNA
sequences, usually obtained through metagenomic studies. Kraken aims
to achieve high sensitivity and high speed by utilizing exact
alignments of k-mers and a novel classification algorithm.

In its fastest mode of operation, for a simulated metagenome of 100 bp
reads, Kraken processed over 4 million reads per minute on a single
core, over 900 times faster than Megablast and over 11 times faster
than the abundance estimation program MetaPhlAn. Kraken's accuracy is
comparable with Megablast, with slightly lower sensitivity and very
high precision.

See the `Kraken home page
<https://ccb.jhu.edu/software/kraken/>`_
for more info.

Let's assign taxonomic labels to our binning results using
Kraken. First, we need to compare the genome bins against the
Kraken database::

  cd ~/workdir/assembly/megahit_out

  qsub -cwd -pe multislot 24 -N maxbin -l mtc=1 -b y \
  kraken --db /vol/metagencourse/krakendb --threads 10 --fasta-input maxbin.001.fasta --output maxbin.001.kraken

  
If you need the full taxonomic name associated with each input
sequence, Kraken provides a script named kraken-translate that produces two
different output formats for classified sequences. The script operates
on the output of kraken::

  kraken-translate --db /vol/metagencourse/krakendb maxbin.001.kraken > maxbin.001.kraken.labels
  
Does the abundance of the bins match the 16S profile of the community?
