Submitting reads
==================

The submission of raw reads can be done programmatically, with the webinterface and using webin-cli. We will focus on the latter solution, see the referenced ENA website for other solutions.

We will need to create a manifest file, which contains the metadata for our read data and references the actual read files that should be submitted.

First, we create another directory::

  mkdir /mnt/submission/assembly/reads
  cd /mnt/submission/assembly/reads

Create the manifest file
^^^^^^^^^^

See this page on details for the content of the manifest file:
https://ena-docs.readthedocs.io/en/latest/submit/reads/webin-cli.html

TODO: which insert size??

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

...

Submit the reads
^^^^^^^^^^^^^^^^

Now, it is time to submit::

  java -jar ....
 
Make sure to use wwwdev to submit to the ENA test server.


References
^^^^^^^^^^
**ENA - Submit Raw Reads** https://ena-docs.readthedocs.io/en/latest/submit/reads.html
