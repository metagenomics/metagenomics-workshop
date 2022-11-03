Submitting an environment sample
==================

There are two ways to submit a sample to ENA (the same as for studies):

1) Using the Webinterface
-----------------------
The Webinterface for the dev submission database can be found at: https://wwwdev.ebi.ac.uk/ena/submit/webin/login

You could follow this guide: https://ena-docs.readthedocs.io/en/latest/submit/samples/interactive.html

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
		<VALUE>stable manure</VALUE>
	      </SAMPLE_ATTRIBUTE>
	    </SAMPLE_ATTRIBUTES>
	  </SAMPLE>
	</SAMPLE_SET>


sequencing method from:
https://ontobee.org/ontology/OBI?iri=http://purl.obolibrary.org/obo/OBI_0400103

broad/local scale environmental context:
http://purl.obolibrary.org/obo/ENVO_00000428

environmental medium:
http://purl.obolibrary.org/obo/ENVO_00010483

taxid from:
https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=408169
...

Submit the sample
^^^^^^^^^^^^^^^^

Now, it is time to submit::

  CHANGE THAT curl -u $ENA_USER:$ENA_PWD -F "SUBMISSION=@submission.xml" -F "PROJECT=@study.xml" "https://wwwdev.ebi.ac.uk/ena/submit/drop-box/submit/"

Make sure to use wwwdev to submit to the ENA test server.


References
^^^^^^^^^^
**ENA - Registering a Sample** https://ena-docs.readthedocs.io/en/latest/submit/samples.html
