Submitting reads
==================

The submission of raw reads can be done programmatically, with the webinterface and using webin-cli. We will focus on the latter solution, see the referenced ENA website for other solutions.

We will need to create a manifest file, which contains the metadata for our read data and references the actual read files that should be submitted.

First, we create another directory::

  mkdir -p /mnt/submission/assembly/reads
  

Then, we ``gzip`` the read files, since they need to be zipped for submission::

  cd /mnt/WGS-data/
  gzip read?.fq
  
And change to our submission directory::
  
  cd /mnt/submission/assembly/reads

Create the manifest file
^^^^^^^^^^

See this page on details for the content of the manifest file:

https://ena-docs.readthedocs.io/en/latest/submit/reads/webin-cli.html

We just use an arbitrary number of 200 for the insert size.

We will use this short manifest template for our submission::

  STUDY the accession number of your submitted study! (TODO)
  SAMPLE the accession number of your submitted sample! (TODO)
  NAME a_unique_experiment_name be creative! (TODO)
  INSTRUMENT Illumina MiSeq
  INSERT_SIZE 200
  LIBRARY_SOURCE GENOMIC
  LIBRARY_SELECTION RANDOM
  LIBRARY_STRATEGY WGS
  FASTQ path_to_fw_read_file (TODO)
  FASTQ path_to_fw_read_file (TODO)
  
Create a file named ``manifest`` and fill it with the content above - fill the fields marked with TODO with the appropriate content. Then continue with the next step.

Validating the read submission
^^^^^^^^^^^^^^^^^^

Before actually submitting, we are validating our manifest file. To do so, we use the option ``-validate`` in our call of ``webin-cli``. Also, make sure, to use the ``-test`` flag to submit to the ENA test server. We also use ``-context=read`` since we are submitting reads. Other options are your ``-username``, ``-password`` and the path to the ``-manifest`` file::

  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=reads -manifest=manifest -validate -test

When everything was successfully validated, you should get a message like::

  INFO : The submission has been validated successfully.


Submit the reads
^^^^^^^^^^^^^^^^

Now, that our read submission is validated successfully, we can go on with the submission. Just replace the ``-validate`` flag by ``-submit`` in the ``webin-cli`` call. Do NOT remove the ``-test`` flag::

  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=reads -manifest=manifest -submit -test
 
If everything works fine, you should receive a message like::

  INFO : The TEST submission has been completed successfully. This was a TEST submission and no data was submitted. The following experiment accession was assigned to  the submission: ERX10008217
  INFO : The TEST submission has been completed successfully. This was a TEST submission and no data was submitted. The following run accession was assigned to the submission: ERR10488906


Now we can go on and submit our assembly.


References
^^^^^^^^^^
**ENA - Submit Raw Reads** https://ena-docs.readthedocs.io/en/latest/submit/reads.html
