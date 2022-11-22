Annotating a MAG and prepare it for ENA submission
=================================

In the next step, we want to submit a fully annotated MAG to ENA. The corresponding checklist ist this one:

https://www.ebi.ac.uk/ena/browser/view/ERC000047

By checking the mandatory fields, we need an information, that is missing so far: completeness and contamination scores. We can get those using the tool ``checkm``.

Computing completeness and contamination using CheckM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Source the environment to make sure, the check database path is set as variable::

  source /etc/environment

Run checkm on all bins (replace the bin folder name with the correct path from your metabat binning)::

  sudo checkm lineage_wf -t 28 -x fa /mnt/WGS-data/megahit_out/metabat/final.contigs.fa.metabat-bins-*/ /mnt/WGS-data/megahit_out/metabat/checkm/ > /mnt/WGS-data/megahit_out/metabat/checkm.log

Now, the results can be found in the file ``checkm.log``::

  tail -20 /mnt/WGS-data/megahit_out/metabat/checkm.log

Note the completeness and contamination values for your MAG, you will need them later. 

Annotation with prokka
^^^^^^^^^^^^^^^^^^^

The multiplex capability and high yield of current day DNA-sequencing instruments has made bacterial whole genome sequencing a routine affair. The subsequent de novo assembly of reads into contigs has been well addressed. The final step of annotating all relevant genomic features on those contigs can be achieved slowly using existing web- and email-based systems, but these are not applicable for sensitive data or integrating into computational pipelines. Prokka is a command line software tool to fully annotate a draft bacterial genome in about 10 min on a typical desktop computer. It produces standards-compliant output files for further analysis or viewing in genome browsers.

``prokka`` is pretty straightforward to use, however, it needs the sequence in unzipped fasta format. Unzip the bin file again::

  gunzip /mnt/WGS-data/megahit_out/metabat/bin.*.fa.gz
  
Check the taxonomy of your bin again, we need the kingdom to call prokka correctly. It probably is a Bacteria (if not, change accordingly to archaea). Then we call Prokka with the bin sequence, the kingdom and specify an output directory::
  
  prokka --kingdom bacteria --cpus 28 /mnt/WGS-data/megahit_out/metabat/bin.*.fa --outdir /mnt/WGS-data/megahit_out/metabat/prokka

Then have look at the output folder::

  ls -l /mnt/WGS-data/megahit_out/metabat/prokka

It contains``.gff`` file that we will use along with the bin fasta file to generate an EMBL compatible flat file now.

Create an EMBL flat file
^^^^^^^^^^^^^^^^^^^^^^^

Unfortunately, prokka does not produce a format, that we can submit to ENA. However, we have all the information we need in the bin fasta and gff3 files. An EMBL compatible flat file can be generated using the tool ``EMBLmyGFF3``. 

An important note: In order to submit annotated sequences to ENA, you would need to get a locus tag prefix for each of your MAGs. See: https://ena-docs.readthedocs.io/en/latest/faq/locus_tags.html

These need to be registered along with your study and take at least 24 hours to be available. The test service however, does not allow registration of locus tags. We just use the placeholder LOCUSTAG instead. 

First we need to change the default python3 version to python3.8 using::

  sudo update-alternatives --config python3
  
Then select the python 3.8 option (2).

The following command yields us an EMBL compatible flat file, you need to fill in some of the fields (correct bin fasta file, study/project accession, and taxid)::

  EMBLmyGFF3 /mnt/WGS-data/megahit_out/metabat/prokka/PROKKA_YOUR_RESULT.gff /mnt/WGS-data/megahit_out/bin.YOURBIN.fa \
        --data_class STD \
        --topology linear \
        --molecule_type "genomic DNA" \
        --transl_table 11  \
        --species TODO: your taxid here! \
        --environmental_sample \
        --isolation_source "forest soil" \
        --locus_tag LOCUSTAG \
        --project_id TODO: PRJXXXXXXX \
        -o /mnt/WGS-data/megahit_out/metabat/mybin.embl

Data class might be HTG as well:
https://ena-docs.readthedocs.io/en/latest/retrieval/general-guide/data-classes.html

Inspect your EMBL file. Then we proceed with the submission of a MAG sample before we submit the generated EMBL file.

References
^^^^^^^^^^

**prokka** http://www.vicbioinformatics.com/software.prokka.shtml

**CheckM** https://github.com/Ecogenomics/CheckM

**EMBLmyGFF3** https://github.com/NBISweden/EMBLmyGFF3
