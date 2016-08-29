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
  
  qsub -cwd -pe multislot 12 -N metaquast -b y \
  /usr/local/bin/metaquast.py --threads 12 --gene-finding --meta \
  -R $HOME/workdir/assembly/genomes/Aquifex_aeolicus_VF5.fna,\
  $HOME/workdir/assembly/genomes/Bdellovibrio_bacteriovorus_HD100.fna,\
  $HOME/workdir/assembly/genomes/Chlamydia_psittaci_MN.fna,\
  $HOME/workdir/assembly/genomes/Chlamydophila_pneumoniae_CWL029.fna,\
  $HOME/workdir/assembly/genomes/Chlamydophila_pneumoniae_J138.fna,\
  $HOME/workdir/assembly/genomes/Chlamydophila_pneumoniae_LPCoLN.fna,\
  $HOME/workdir/assembly/genomes/Chlamydophila_pneumoniae_TW_183.fna,\
  $HOME/workdir/assembly/genomes/Chlamydophila_psittaci_C19_98.fna,\
  $HOME/workdir/assembly/genomes/Finegoldia_magna_ATCC_29328.fna,\
  $HOME/workdir/assembly/genomes/Fusobacterium_nucleatum_ATCC_25586.fna,\
  $HOME/workdir/assembly/genomes/Helicobacter_pylori_26695.fna,\
  $HOME/workdir/assembly/genomes/Lawsonia_intracellularis_PHE_MN1_00.fna,\
  $HOME/workdir/assembly/genomes/Mycobacterium_leprae_TN.fna,\
  $HOME/workdir/assembly/genomes/Porphyromonas_gingivalis_W83.fna,\
  $HOME/workdir/assembly/genomes/Wigglesworthia_glossinidia.fna \
  -o quast \
  -l MegaHit,Ray_31,velvet_31,velvet_51,idba_ud \
  megahit_out/final.contigs.fa \
  ray_31/Contigs.fasta \
  velvet_31/contigs.fa \
  velvet_51/contigs.fa \
  idba_ud_out/contig.fa

QUAST generates HTML reports including a number of interactive graphics. To access these reports, copy the
quast directory to your `public_html` folder::

  cp -r quast ~/public_html

After that, you can load the reports in your web browser::

  http://YOUR_OPENSTACK_INSTANCE_IP/~ubuntu/quast/summary/report.html
  http://YOUR_OPENSTACK_INSTANCE_IP/~ubuntu/quast/combined_quast_output/report.html
