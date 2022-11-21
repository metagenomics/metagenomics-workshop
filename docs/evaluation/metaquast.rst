MetaQUAST
=========

QUAST stands for QUality ASsessment Tool. The tool evaluates genome
assemblies by computing various metrics.  You can find all project
news and the latest version of the tool at `sourceforge
<http://sourceforge.net/projects/quast>`_.  QUAST utilizes MUMmer,
GeneMarkS, GeneMark-ES, GlimmerHMM, and GAGE. In addition, MetaQUAST
uses MetaGeneMark, Krona tools, BLAST, and SILVA 16S rRNA
database. See the `metaQuast home page <http://quast.sourceforge.net/metaquast//>`_
for more info.

In case not all assemblies finished so far, copy the pre-computed
assembly results to your local directory::

  cd /mnt/WGS-data
  wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/denbi-mg-course/assembly_results.tar
  tar xvf assembly_results.tar
  cp -v -r /mnt/WGS-data/assembly_results/* .

To call ``metaquast.py`` we have to provide reference genomes which
are used to calculate a number of different metrics for evaluation of
the assembly. In real-world metagenomics, these references are usually
not available, of course::

  cd /mnt/WGS-data
  
  metaquast.py --threads 28 --gene-finding \
  -R /mnt/WGS-data/genomes/Aquifex_aeolicus_VF5.fna,\
  /mnt/WGS-data/genomes/Bdellovibrio_bacteriovorus_HD100.fna,\
  /mnt/WGS-data/genomes/Chlamydia_psittaci_MN.fna,\
  /mnt/WGS-data/genomes/Chlamydophila_pneumoniae_CWL029.fna,\
  /mnt/WGS-data/genomes/Chlamydophila_pneumoniae_J138.fna,\
  /mnt/WGS-data/genomes/Chlamydophila_pneumoniae_LPCoLN.fna,\
  /mnt/WGS-data/genomes/Chlamydophila_pneumoniae_TW_183.fna,\
  /mnt/WGS-data/genomes/Chlamydophila_psittaci_C19_98.fna,\
  /mnt/WGS-data/genomes/Finegoldia_magna_ATCC_29328.fna,\
  /mnt/WGS-data/genomes/Fusobacterium_nucleatum_ATCC_25586.fna,\
  /mnt/WGS-data/genomes/Helicobacter_pylori_26695.fna,\
  /mnt/WGS-data/genomes/Lawsonia_intracellularis_PHE_MN1_00.fna,\
  /mnt/WGS-data/genomes/Mycobacterium_leprae_TN.fna,\
  /mnt/WGS-data/genomes/Porphyromonas_gingivalis_W83.fna,\
  /mnt/WGS-data/genomes/Wigglesworthia_glossinidia.fna \
  -o quast \
  -l MegaHit,metaSPAdes,Ray_31,Ray_51,velvet_31,velvet_51,idba_ud \
  megahit_out/final.contigs.fa \
  metaspades_out/contigs.fasta \
  ray_31/Contigs.fasta \
  ray_51/Contigs.fasta \
  velvet_31/contigs.fa \
  velvet_51/contigs.fa \
  idba_ud_out/contig.fa

QUAST generates HTML reports including a number of interactive graphics. To access these reports,
load the reports in your web browser::

  firefox quast/report.html


