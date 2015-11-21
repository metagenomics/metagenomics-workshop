MetaQUAST
=========

QUAST stands for QUality ASsessment Tool. The tool evaluates genome
assemblies by computing various metrics.  You can find all project
news and the latest version of the tool at `sourceforge
<http://sourceforge.net/projects/quast>`_.  QUAST utilizes MUMmer,
GeneMarkS, GeneMark-ES, GlimmerHMM, and GAGE. In addition, MetaQUAST
uses MetaGeneMark, Krona tools, BLAST, and SILVA 16S rRNA
database. See the `QUAST home page <http://quast.bioinf.spbau.ru//>`_
for more info.

To call ``metaquast.py`` we have to provide reference genomes which
are used to calculate a number of different metrics for evaluation of
the assembly. In real-world metagenomics, these references are usually
not available, of course::

  cd ~/workdir/assembly
  
  qsub -cwd -pe multislot 24 -N metaquast -l mtc=1 -b y \
  /vol/cmg/bin/metaquast.py --threads 24 --gene-finding --meta \
  -R /vol/metagencourse/DATA/WGS-data/genomes/Aquifex_aeolicus_VF5.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Bdellovibrio_bacteriovorus_HD100.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Chlamydia_psittaci_MN.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Chlamydophila_pneumoniae_CWL029.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Chlamydophila_pneumoniae_J138.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Chlamydophila_pneumoniae_LPCoLN.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Chlamydophila_pneumoniae_TW_183.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Chlamydophila_psittaci_C19_98.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Finegoldia_magna_ATCC_29328.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Fusobacterium_nucleatum_ATCC_25586.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Helicobacter_pylori_26695.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Lawsonia_intracellularis_PHE_MN1_00.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Mycobacterium_leprae_TN.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Porphyromonas_gingivalis_W83.fna,\
  /vol/metagencourse/DATA/WGS-data/genomes/Wigglesworthia_glossinidia.fna \
  -o quast \
  -l MegaHit,Ray_31,velvet_31,velvet_51,idba_ud \
  megahit_out/final.contigs.fa \
  ray_31/Contigs.fasta \
  velvet_31/contigs.fa \
  velvet_51/contigs.fa \
  idba_ud_out/contig.fa

QUAST generates HTML reports including a number of interactive graphics. 
You can load the reports into your web browser::

  firefox quast/summary/report.html
  firefox quast/combined_quast_output/report.html


