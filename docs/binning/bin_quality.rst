Assessing bin quality
===============

To get an impression about the quality of our bins, we compute the completeness and contamination values for our bins. 

Computing completeness and contamination using CheckM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CheckM provides a set of tools for assessing the quality of genomes recovered from isolates, single cells, or metagenomes. It provides robust estimates of genome completeness and contamination by using collocated sets of genes that are ubiquitous and single-copy within a phylogenetic lineage. Assessment of genome quality can also be examined using plots depicting key genomic characteristics (e.g., GC, coding density) which highlight sequences outside the expected distributions of a typical genome. CheckM also provides tools for identifying genome bins that are likely candidates for merging based on marker set compatibility, similarity in genomic characteristics, and proximity within a reference genome tree.
See the `CheckM home page <https://ecogenomics.github.io/CheckM/>`_ for more info.

Run checkm on all bins::

  cd /mnt/megahit_out/metabat/

  checkm lineage_wf -t 28 -x fa final.contigs.fa.metabat-bins-*/ checkm_metabat/ > ../checkm_metabat.log



And the same for the maxbin results::

  cd /mnt/megahit_out/maxbin/

  checkm lineage_wf -t 28 -x fasta . checkm_maxbin > ../check_maxbin.log  


Now, the results can be found in the file ``checkm_metabat.log`` and ``checkm_maxbin.log``::

  cd /mnt/megahit_out/

  tail -20 checkm_metabat.log
  tail -20 checkm_maxbin.log



