Assembly Evaluation using MetaQUAST
===================================

We are going to evaluate our assemblies using the reference genomes.

Call `metaquast`::

  python ~/quast-3.1/metaquast.py --threads 16 --gene-finding --meta -R \
  megahit_out/final.contigs.fa \
  ray_31/Contigs.fasta \
  velvet_31/contigs.fa \
  -l MegaHit,Ray_31,velvet_31 \
  /mnt/References/Helicobacter_pylori_2017_uid161151.fna,\
  /mnt/References/Chlamydia_trachomatis_F_SW5_uid167485.fna,\
  /mnt/References/Chlamydia_trachomatis_F_SW4_uid167484.fna,\
  /mnt/References/Staphylococcus_aureus_CN1_uid217769.fna,\
  /mnt/References/Staphylococcus_aureus_11819_97_uid159981.fna,\
  /mnt/References/Listeria_monocytogenes_J0161_uid54459.fna,\
  /mnt/References/Streptococcus_pneumoniae_Hungary19A_6_uid59117.fna \
  -o quast


