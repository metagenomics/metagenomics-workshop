Annotating a MAG and prepare it for ENA submission
=================================

In the next step, we want to submit a fully annotated MAG to ENA. The corresponding checklist ist this one:

https://www.ebi.ac.uk/ena/browser/view/ERC000047

By checking the mandatory fields, we need an information, that is missing so far: completeness and contamination scores. We can get those using the tool ``checkm``.

Computing completeness and contamination using CheckM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

TODO....

Annotation with prokka
^^^^^^^^^^^^^^^^^^^

The multiplex capability and high yield of current day DNA-sequencing instruments has made bacterial whole genome sequencing a routine affair. The subsequent de novo assembly of reads into contigs has been well addressed. The final step of annotating all relevant genomic features on those contigs can be achieved slowly using existing web- and email-based systems, but these are not applicable for sensitive data or integrating into computational pipelines. Prokka is a command line software tool to fully annotate a draft bacterial genome in about 10 min on a typical desktop computer. It produces standards-compliant output files for further analysis or viewing in genome browsers.

``prokka`` is pretty straightforward to use, however, it needs the sequence in unzipped fasta format. Unzip the bin file again::

  gunzip /mnt/WGS-data/megahit_out/metabat/bin.*.fa.gz
  
Check the taxonomy of your bin again, we need the kingdom to call prokka correctly. It probably is a Bacteria (if not, change accordingly to archaea. Then we call Prokka with the bin sequence, the kingdom and specify an output directory::
  
  prokka --kingdom bacteria --cpus 28 /mnt/WGS-data/megahit_out/metabat/bin.*.fa --outdir /mnt/WGS-data/megahit_out/metabat/prokka

Then have look at the output folder::

  ls -l /mnt/WGS-data/megahit_out/metabat/prokka

It contains a ``.ffn`` file and a ``.gff`` file. We will use those files to generate an EMBL compatible flat file now.

Create an EMBL flat file
^^^^^^^^^^^^^^^^^^^^^^^

Unfortunately, prokka does not produce a format, that we can submit to ENA. However, we have all the information we need in the fasta and gff3 files. An EMBL compatible flat file can be generated using the tool ``EMBLmyGFF3``. 

TODO: command


References
^^^^^^^^^^

**prokka** http://www.vicbioinformatics.com/software.prokka.shtml
**CheckM** https://github.com/Ecogenomics/CheckM
**EMBLmyGFF3** https://github.com/NBISweden/EMBLmyGFF3
