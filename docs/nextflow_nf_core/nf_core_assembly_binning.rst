nf-core assembly and binning
================

We will use nf-core/mag workflow for metagenomics assembly and binning. It starts from reads quality control using ``fastp``, and ``FastQC``. Then:

- assigns taxonomy to reads using ``Centrifuge`` and/or ``Kraken2``
- performs assembly using ``MEGAHIT`` and ``SPAdes``, and checks their quality using ``Quast``
- (optionally) performs ancient DNA assembly validation using ``PyDamage`` and contig consensus sequence recalling with ``Freebayes`` and ``BCFtools``
- predicts protein-coding genes for the assemblies using ``Prodigal``, and bins with ``Prokka`` and optionally ``MetaEuk``
- performs metagenome binning using ``MetaBAT2``, ``MaxBin2``, and/or with ``CONCOCT``, and checks the quality of the genome bins using ``Busco``, or ``CheckM``, and optionally ``GUNC``.
- Performs ancient DNA validation and repair with ``pyDamage`` and ``Freebayes``
- optionally refines bins with ``DasTool``
- assigns taxonomy to bins using ``GTDB-Tk`` and/or ``CAT`` and optionally identifies viruses in assemblies using ``geNomad``, or Eukaryotes with ``Tiara``

-------

Before running the workflow, we need to prepare the compressed fastq files as input::

  cd /mnt/WGS-data
  pigz -k read1.fq
  pigz -k read2.fq

Then we can start the mag workflow as follows::

  cd ..
  mkdir -p output_mag
  nextflow run nf-core/mag \
    -profile singularity \
    --input 'WGS-data/read{1,2}.fq.gz' \
    --outdir output_mag \
    --skip_concoct \
    --skip_metaeuk \
    --skip_prokka \
    --skip_prodigal \
    --skip_spades \
    --skip_metabat2 \
    --skip_gtdbtk \
    --skip_binqc

