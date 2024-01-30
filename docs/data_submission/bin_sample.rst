Submitting a bin sample
==================

For every bin we like to submit, we will need to create a  bin sample. That bin sample should be linked to the environmental sample.

As before, we will rely upon the programmatical submission using ``curl`` and an XML file.

First, create a work folder for submissions and a subfolder for the sample files::

  mkdir -p /mnt/submission/bins/sample/
  cd /mnt/submission/bins/sample

Create submission.xml
^^^^^^^^^^
The next thing you need to to is to create a file submission.xml with the following content (same as before so you could just copy the file from previous submissions)::
  
  <SUBMISSION>
     <ACTIONS>
        <ACTION>
           <ADD/>
        </ACTION>
     </ACTIONS>
  </SUBMISSION>

You can use an editor like ``gedit`` to do so. It is actually the same file as the submission.xml for the study (except the HOLD part) so you could just copy that as well.

Get the correct ENA checklist
^^^^^^^^^^

The following checklist should be used for binned assemblies:

https://www.ebi.ac.uk/ena/browser/view/ERC000050


Create sample.xml
^^^^^^^^^^

There are a number of fields to be filled. You can download the XML file to see what can be filled out. Since this is a test submission, 
we will reduce that to the mandatory fields only, and we can copy some values from our previous environmental sample submission.

However, you will need to fill the taxon fields yourself. Have a look in the GTDBtk results, look for your bin, and search the taxa in the NCBI taxonomy:

https://www.ncbi.nlm.nih.gov/taxonomy

Find out the taxid, common name and scientific name for your bin and fill the information in the XML file::

	<SAMPLE_SET>
	  <SAMPLE alias="course_test_bin_sample">
	    <TITLE>Bin sample for the metagenomic course 2022</TITLE>
	    <SAMPLE_NAME>
	      <TAXON_ID>TODO: your taxid</TAXON_ID>
	      <SCIENTIFIC_NAME>TODO: taxons name</SCIENTIFIC_NAME>
	      <COMMON_NAME>TODO: taxons name</COMMON_NAME>
	    </SAMPLE_NAME>
	    <DESCRIPTION>DESCRIPTION</DESCRIPTION>
	    <SAMPLE_ATTRIBUTES>
	      <SAMPLE_ATTRIBUTE>
	        <TAG>ENA-CHECKLIST</TAG>
		<VALUE>ERC000050</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>project name</TAG>
		<VALUE>MGCourse 2022</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
	        <TAG>sequencing method</TAG>
		<VALUE>MiSeq</VALUE>
	      </SAMPLE_ATTRIBUTE>
              <SAMPLE_ATTRIBUTE>
	        <TAG>assembly software</TAG>
		<VALUE>MEGAHIT</VALUE>
	      </SAMPLE_ATTRIBUTE>
              <SAMPLE_ATTRIBUTE>
	        <TAG>binning software</TAG>
		<VALUE>METABAT</VALUE>
	      </SAMPLE_ATTRIBUTE>
              <SAMPLE_ATTRIBUTE>
	        <TAG>investigation type</TAG>
		<VALUE>metagenome</VALUE>
	      </SAMPLE_ATTRIBUTE>
              <SAMPLE_ATTRIBUTE>
	        <TAG>binning parameters</TAG>
		<VALUE>default</VALUE>
	      </SAMPLE_ATTRIBUTE>
              <SAMPLE_ATTRIBUTE>
	        <TAG>isolation source</TAG>
		<VALUE>forest soil</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>collection date</TAG>
		<VALUE>2022-11-03</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>geographic location (country and/or sea)</TAG>
		<VALUE>Germany</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>geographic location (latitude)</TAG>
		<VALUE>52.019101</VALUE>
		<UNITS>DD</UNITS>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>geographic location (longitude)</TAG>
		<VALUE>8.531007</VALUE>
		<UNITS>DD</UNITS>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>broad-scale environmental context</TAG>
		<VALUE>temperate woodland</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>local environmental context</TAG>
		<VALUE>temperate woodland</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>environmental medium</TAG>
		<VALUE>forest soil</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>sample derived from</TAG>
		<VALUE>TODO: you environmental sample accession here!</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		<TAG>metagenomic source</TAG>
		<VALUE>outdoor metagenome</VALUE>
	      </SAMPLE_ATTRIBUTE>
	    </SAMPLE_ATTRIBUTES>
	  </SAMPLE>
	</SAMPLE_SET>

Don't forget to fill in your environmental sample accession in the appropriate field.

Note that you would need to add one sample for each of your bins, if you would like to submit all of them! In our case, we will only submit one bin for demonstration purposes.

Submit the sample
^^^^^^^^^^^^^^^^

Now, it is time to submit::
  
  cd /mnt/submission/bins/sample
  curl -u $ENA_USER:$ENA_PWD -F "SUBMISSION=@submission.xml" -F "SAMPLE=@sample.xml" "https://wwwdev.ebi.ac.uk/ena/submit/drop-box/submit/" > receipt.xml

Make sure to use wwwdev to submit to the ENA test server.

Get the sample accession number
^^^^^^^^^^^^^^^

The response is stored in the file "receipt.xml". You can find the accession number for your sample in this line::

  <SAMPLE accession="ERS13654528" alias="course_test_environmental sample" status="PRIVATE">
  
Also note, that this number is only valid for today (as for the study accession), since it is discarded after 24 hours::

     <MESSAGES>
          <INFO>This submission is a TEST submission and will be discarded within 24 hours</INFO>
     </MESSAGES>

Note your bin sample accession number somewhere, you will need it for the next steps.

Now let's submit our bin for this sample.


References
^^^^^^^^^^
**ENA - Submitting Binned Metagenome Assemblies** https://ena-docs.readthedocs.io/en/latest/submit/assembly/metagenome/binned.html
**ENA - Registering a Sample** https://ena-docs.readthedocs.io/en/latest/submit/samples.html
