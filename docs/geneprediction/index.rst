***************
Gene Prediction
***************

Prodigal (Prokaryotic Dynamic Programming Genefinding Algorithm) is a
microbial (bacterial and archaeal) gene finding program developed at
Oak Ridge National Laboratory and the University of Tennessee. See the
`Prodigal home page <http://prodigal.ornl.gov/>`_ for more info.

To run ``prodigal`` on our data, simply type::

  cd /vol/spool/tutorial-data/megahit_out
  prodigal -p meta -a final.contigs.genes.faa -d final.contigs.genes.fna -f gff -o final.contigs.genes.gff -i final.contigs.fa

Output files:

+------------------+----------------------------------------------------+
| final.contigs.genes.gff | positions of predicted genes in GFF format  |
+------------------+----------------------------------------------------+
| final.contigs.genes.faa | protein translations of predicted genes     |
+------------------+----------------------------------------------------+
| final.contigs.genes.fna | nucleotide sequences of predicted genes     |
+------------------+----------------------------------------------------+



.. toctree::
   :maxdepth: 1


