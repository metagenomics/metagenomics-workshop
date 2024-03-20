Assessing bin quality
===============

To get an impression about the quality of our bins, we compute the completeness and contamination values for our bins. 

Computing completeness and contamination using CheckM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CheckM provides a set of tools for assessing the quality of genomes recovered from isolates, single cells, or metagenomes. It provides robust estimates of genome completeness and contamination by using collocated sets of genes that are ubiquitous and single-copy within a phylogenetic lineage. Assessment of genome quality can also be examined using plots depicting key genomic characteristics (e.g., GC, coding density) which highlight sequences outside the expected distributions of a typical genome. CheckM also provides tools for identifying genome bins that are likely candidates for merging based on marker set compatibility, similarity in genomic characteristics, and proximity within a reference genome tree.

Run checkm on all bins (replace the bin folder name with the correct path from your metabat binning)::

  sudo checkm lineage_wf -t 28 -x fa /mnt/WGS-data/megahit_out/metabat/final.contigs.fa.metabat-bins-*/ /mnt/WGS-data/megahit_out/metabat/checkm/ > /mnt/WGS-data/megahit_out/metabat/checkm.log

Now, the results can be found in the file ``checkm.log``::

  tail -20 /mnt/WGS-data/megahit_out/metabat/checkm.log





https://ecogenomics.github.io/CheckM/
