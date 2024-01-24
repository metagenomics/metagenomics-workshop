Submitting an environment sample
==================

There are two ways to submit a sample to ENA (the same as for studies):

1) Using the Webinterface
-----------------------
The Webinterface for the dev submission database can be found at: 

https://wwwdev.ebi.ac.uk/ena/submit/webin/login

You could follow this guide: 

https://ena-docs.readthedocs.io/en/latest/submit/samples/interactive.html

Download the following file: 
https://github.com/metagenomics/metagenomics-workshop/blob/denbi_nfdi_simplevm/files/environmental_sample.tsv

and submit it in the webinterface as described above. 

Samples can be submitted programmatically was well as described below (for reference), we will do that for the bin samples later.

2) Registering a sample programmatically
-----------------------
... using the linux command line tool ``curl``.

As for the study submission, we will also use this approach in this short course. 

First, create a work folder for submissions and a subfolder for the sample files::

  mkdir -p /mnt/submission/assembly/sample/
  cd /mnt/submission/assembly/sample

Create submission.xml
^^^^^^^^^^
The next thing you need to to is to create a file submission.xml with the following content::
  
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

The next thing, you need to do, is to identify the correct checklist for your sample. Checklists can be browsed here, look for example for "environmental":
https://www.ebi.ac.uk/ena/browser/checklists

Since we have an artifical dataset let's choose this checklist for example:
https://www.ebi.ac.uk/ena/browser/view/ERC000025


Create sample.xml
^^^^^^^^^^

There are a number of fields to be filled. You can download the XML file to see what can be filled out. Since this is a test submission, 
we will reduce that to the mandatory fields only::

	<SAMPLE_SET>
	  <SAMPLE alias="course_test_environmental sample">
	    <TITLE>Environmental sample for the metagenomic course 2022</TITLE>
	    <SAMPLE_NAME>
	      <TAXON_ID>1839947</TAXON_ID>
	      <SCIENTIFIC_NAME>outdoor metagenome</SCIENTIFIC_NAME>
	      <COMMON_NAME>outdoor metagenome</COMMON_NAME>
	    </SAMPLE_NAME>
	    <DESCRIPTION>DESCRIPTION</DESCRIPTION>
	    <SAMPLE_ATTRIBUTES>
	      <SAMPLE_ATTRIBUTE>
		<TAG>ENA-CHECKLIST</TAG>
		<VALUE>ERC000025</VALUE>
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
	    </SAMPLE_ATTRIBUTES>
	  </SAMPLE>
	</SAMPLE_SET>


Some notes on the selected values:

The sequencing method is choosen from the following recommended vocabulary:
https://ontobee.org/ontology/OBI?iri=http://purl.obolibrary.org/obo/OBI_0400103

The broad/local scale environmental context is choosen from the following recommended vocabulary:
http://purl.obolibrary.org/obo/ENVO_00000428

The environmental medium is choosen from the following recommended vocabulary:
http://purl.obolibrary.org/obo/ENVO_00010483

There are several designated taxids in the NCBI taxonomy for metagenomes. Here is a list:
https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=408169

The chosen values in our example are of course fictitious.

Submit the sample
^^^^^^^^^^^^^^^^

Now, it is time to submit::
  
  cd /mnt/submission/assembly/sample
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

Note your accession number somewhere, you will need it for the next steps.

Now let's submit our reads for this study.



References
^^^^^^^^^^
**ENA - Registering a Sample** https://ena-docs.readthedocs.io/en/latest/submit/samples.html
