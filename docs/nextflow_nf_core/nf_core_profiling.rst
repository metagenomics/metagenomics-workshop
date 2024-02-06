nf-core pipeline for taxonomy profiling
================

The nf-core/taxpfoiler (https://nf-co.re/taxprofiler) will be used in this training. It consists of serveral best practice profilers: e.g., ``mOTUs`` and ``metaPhlAn``.

- **Download reference databases**

.. code-block:: shell

  cd /mnt

  wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/mg_databases/db_mOTU_v3.1.0.tar.gz
  tar zvxf db_mOTU_v3.1.0.tar.gz

  mkdir -p output_taxprofiler

- **Set the database path with** ``vi databases.csv``

.. code-block:: shell

  tool,db_name,db_params,db_path
  motus,db_mOTU,,/mnt/db_mOTU

- **Prepare sample sheet file with** ``vi samples.csv``

.. code-block:: shell

  sample,run_accession,instrument_platform,fastq_1,fastq_2,fasta
  s1,run1,ILLUMINA,/mnt/WGS-data/read1.fq.gz,/mnt/WGS-data/read2.fq.gz,


- **Run the pipeline**

.. code-block:: shell

  nextflow run nf-core/taxprofiler \
    --input samples.csv \
    --databases databases.csv \
    --outdir output_taxprofiler \
    -profile singularity \
    --run_motus \
    --motus_use_relative_abundance

After the pipeline finished, we can will have all results in the ``output_taxprofiler`` directory.
