Submitting a metagenome bin
==================

The submission of the bin can be done only using ``webin-cli``.

Again, We will need to create a manifest file, which contains the metadata for our read data and references the assembly ``fasta`` file that should be submitted.

First, we create another directory::

  mkdir -p /mnt/submission/bins/bins

Now, choose one of the bin files from the metabat results in ``/mnt/WGS-data/megahit_out/metabat/final.contigs.fa.metabat-bins-*/`` and copy it to the metabat folder::

  cp <your_bin> /mnt/WGS-data/megahit_out/metabat/
  
Then, we ``gzip`` the bin file, since it needs to be zipped for submission::
  
  gzip /mnt/WGS-data/megahit_out/metabat/bin.*.fa
  
And change to our submission directory::
  
  cd /mnt/submission/bins/bins

Create the manifest file
^^^^^^^^^^

We will use this short manifest template for our submission (almost the same as the assembly except for the 'binned metagenome' and different fasta file ofr course), fill in YOUR values for STUDY, SAMPLE and RUN accession, be careful to fill in your BINNED SAMPLE ACCESSION, not the environmental sample accession::

  STUDY   TODO
  SAMPLE   TODO
  RUN_REF   TODO
  ASSEMBLYNAME   TODO
  ASSEMBLY_TYPE   binned metagenome
  COVERAGE   20
  PROGRAM   MEGAHIT
  PLATFORM   ILLUMINA
  MOLECULETYPE   genomic DNA
  FASTA  /mnt/WGS-data/megahit_out/metabat/bin.*.fa.gz
  
Create a file named ``manifest`` and fill it with the content above - fill the fields marked with TODO with the appropriate content. Then continue with the next step.

Validating the bin submission
^^^^^^^^^^^^^^^^^^

Before actually submitting, we are validating our manifest file. To do so, we use the option ``-validate`` in our call of ``webin-cli``. Also, make sure, to use the ``-test`` flag to submit to the ENA test server. We also use ``-context=genome`` since we are submitting an assembly. Other options are your ``-username``, ``-password`` and the path to the ``-manifest`` file::
  
  cd /mnt/submission/bins/bins
  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=genome -manifest=manifest -validate -test

When everything was successfully validated, you should get a message like::

  INFO : The submission has been validated successfully.


Submit the bin
^^^^^^^^^^^^^^^^

Now, that our bin submission is validated successfully, we can go on with the submission. Just replace the ``-validate`` flag by ``-submit`` in the ``webin-cli`` call. Do NOT remove the ``-test`` flag::

  cd /mnt/submission/bins/bins
  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=genome -manifest=manifest -submit -test
 
If everything works fine, you should receive a message like::

INFO : The TEST submission has been completed successfully. This was a TEST submission and no data was submitted. The following analysis accession was assigned to the submission: ERZ14243535

Great! Now let's go on by adding a MAG to this submission.


References
^^^^^^^^^^
**ENA - Submitting Binned Metagenome Assemblies** https://ena-docs.readthedocs.io/en/latest/submit/assembly/metagenome/binned.html
