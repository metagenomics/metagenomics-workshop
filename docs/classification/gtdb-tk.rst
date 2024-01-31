Genome Taxonomy Database (GTDB)
===============

GTDB-Tk is a software toolkit for assigning objective taxonomic 
classifications to bacterial and archaeal genomes based on the 
`Genome Database Taxonomy GTDB <https://gtdb.ecogenomic.org>`_. 
It is designed to work with recent 
advances that allow hundreds or thousands of metagenome-assembled 
genomes (MAGs) to be obtained directly from environmental samples. 
It can also be applied to isolate and single-cell genomes. 

See the `GTDBTk homepage <https://ecogenomics.github.io/GTDBTk/index.html>`_ 
for more info.

First, we need to download the GTDB database files. The database is pretty
big (64 Gb), so even downloading it from our local copy in the de.NBI Cloud
will take a couple of minutes. After downloading, we need to extract the
tar archive (please be patient ;)::

  cd /mnt
  wget -qO- https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/denbi-mg-course/gtdbtk_v2_data.tar.gz | tar xvz
   ub
Now we need to set an environment variable that stores the path to
the database and put GTDBtk in our path::

  export GTDBTK_DATA_PATH=/mnt/release207_v2
  
Next, let's assign taxonomic labels to our binning results using
GTDB-Tk::

  cd /mnt/WGS-data/megahit_out/maxbin
  gtdbtk classify_wf --extension fasta --cpus 28 --genome_dir . --out_dir gtdbtk_out --mash_db /mnt/release207_v2/mash.msh

When you are done, also compute the classification for the metabat binning, since we will need the results tomorrow for the submission::

  cd /mnt/WGS-data/megahit_out/metabat/final.contigs.fa.metabat-bins...YOUR_FOLDERNAME
  gtdbtk classify_wf --extension fa --cpus 28 --genome_dir . --out_dir gtdbtk_out --mash_db /mnt/release207_v2/mash.msh

Load gtdbtk.backbone.bac120.classify.tree, gtdbtk.bac120.classify.tree.7.tree into the ncbi taxonomy viewer:

https://www.ncbi.nlm.nih.gov/tools/treeviewer/

Convert to itol format::

  gtdbtk convert_to_itol --input_tree gtdbtk_out/classify/gtdbtk.backbone.bac120.classify.tree --output_tree test.itol

Load into:

https://itol.embl.de/upload.cgi
