Velvet Assembly
===============

Velvet was one of the first de novo genomic assemblers specially designed for short read sequencing technologies. It was  developed by Daniel Zerbino and Ewan Birney at the European Bioinformatics Institute (EMBL-EBI). Velvet currently takes in short read sequences, removes errors then produces high quality unique contigs. It then uses paired-end read and long read information, when available, to retrieve the repeated areas between contigs. See the Velvet_ home page for more info.



::

  velveth velvet_31 31 -shortPaired -fastq -separate all1.fq all2.fq >& velveth.log &

velvetg::

  velvetg velvet_31 -cov_cutoff auto -ins_length 270 -min_contig_lgth 500 -exp_cov auto >& velvetg.log &

The output is located in the `velvet_31` directory.


.. Velvet: https://www.ebi.ac.uk/~zerbino/velvet/
