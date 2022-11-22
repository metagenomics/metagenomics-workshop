Submitting a MAG
==================

The submission of the MAG can be done only using ``webin-cli``.

Again, We will need to create a manifest file, which contains the metadata for our read data and references the flat file we created during the annotation steps.

First, we create another directory::

  mkdir /mnt/submission/mags/mags

Then, we ``gzip`` the embl file, since it needs to be zipped for submission::
  
  gzip /mnt/WGS-data/megahit_out/metabat/mybin.embl
  
And change to our submission directory::
  
  cd /mnt/submission/mags/mags
  
   
Create the manifest file
^^^^^^^^^^

We will use this short manifest template for our submission (almost the same as the bin except for the 'Metagenome-Assembled Genome (MAG)' and the flat file), fill in YOUR values for STUDY, SAMPLE and RUN accession, be careful to fill in your MAG SAMPLE ACCESSION, not the environmental or bin sample accession::

  STUDY   TODO
  SAMPLE   TODO
  RUN_REF   TODO
  ASSEMBLYNAME   TODO
  ASSEMBLY_TYPE   Metagenome-Assembled Genome (MAG)
  COVERAGE   20
  PROGRAM   MEGAHIT
  PLATFORM   ILLUMINA
  MOLECULETYPE   genomic DNA
  DESCRIPTION   TODO
  FLATFILE   /mnt/WGS-data/megahit_out/metabat/mybin.embl.gz
  
Create a file named ``manifest`` and fill it with the content above - fill the fields marked with TODO with the appropriate content. Then continue with the next step.

Validating the MAG submission
^^^^^^^^^^^^^^^^^^

Before actually submitting, we are validating our manifest file. To do so, we use the option ``-validate`` in our call of ``webin-cli``. Also, make sure, to use the ``-test`` flag to submit to the ENA test server. We also use ``-context=genome`` since we are submitting an assembly. Other options are your ``-username``, ``-password`` and the path to the ``-manifest`` file::
  
  cd /mnt/submission/mags/mags
  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=genome -manifest=manifest -validate -test

Unfortunately, we get an error::

  ERROR: Submission validation failed because of a user error. Please check validation reports for further information: /mnt/submission/mags/mags/genome/mgcourse2022_mag6/validate

Check the file ``/mnt/submission/mags/mags/genome/mgcourse2022_mag6/validate/mybin.embl.gz.report`` (it's different on your system - the assemblyname is in the path)::

  less /mnt/submission/mags/mags/genome/mgcourse2022_mag6/validate/mybin.embl.gz.report
  
It should contain many lines like this::

  ERROR: Illegal /locus_tag value "LOCUSTAG_MJBABNOI_00673 ". locus_tag prefix "LOCUSTAG" is not registered with the project. [ line: 45893 of mybin.embl.gz]

This is because we didn't register any locus tag prefixes for our study. Since we are using the test submission server, we cannot proceed here. However, you can still check, if there are any other errors in the validation file - if not, the file is theoretically fine to submit and in a real case you could proceed to submit to the production service.

However... ending the example like this is unsatisfying, so we might at least submit the fasta as MAG, although you wouldn't do this in a real project, since everything is already submitted as a bin. 

Change the line::

  FLATFILE   /mnt/WGS-data/megahit_out/metabat/mybin.embl.gz
    
to (change to your bin-ID)::

  FASTA   /mnt/WGS-data/megahit_out/metabat/bin.*.fa.gz
  
make sure, it is zipped::

  gzip /mnt/WGS-data/megahit_out/metabat/bin.*.fa.gz  

And validate again::

  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=genome -manifest=manifest -validate -test
  
This should yield a success message.

Submit the MAG
^^^^^^^^^^^^^^^^

Now, that our MAG submission is validated successfully, we can go on with the submission. Just replace the ``-validate`` flag by ``-submit`` in the ``webin-cli`` call. Do NOT remove the ``-test`` flag::

  cd /mnt/submission/mags/mags
  java -jar ~/webin-cli-5.2.0.jar -username=$ENA_USER -password=$ENA_PWD -context=genome -manifest=manifest -submit -test
 
If everything works fine, you should receive a message like::

INFO : The TEST submission has been completed successfully. This was a TEST submission and no data was submitted. The following analysis accession was assigned to the submission: ERZ14243535

Now the last thing, we could do, is checking your submission in the webinterface:

https://wwwdev.ebi.ac.uk/ena/submit/webin/


References
^^^^^^^^^^
**ENA - Submitting A Metagenome-Assembled Genome (MAG)** https://ena-docs.readthedocs.io/en/latest/submit/assembly/metagenome/binned.html
