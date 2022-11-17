Submitting a MAG sample
==================

For every MAG we like to submit, we will need to create a  bin sample. That MAG sample should be linked to the bin sample.

As before, we will rely upon the programmatical submission using ``curl`` and an XML file.

First, create a work folder for submissions and a subfolder for the sample files::

  mkdir -p /mnt/submission/mags/sample/
  cd /mnt/submission/mags/sample

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

You can use an editor like ``gedit`` to do so. It is actually the same file as the submission.xml for the bin sample so you could just copy that as well.

Get the correct ENA checklist
^^^^^^^^^^

The following checklist should be used for MAG assemblies:
https://www.ebi.ac.uk/ena/browser/view/ERC000047


Create sample.xml
^^^^^^^^^^

TODO: format xml

There are a number of fields to be filled. You can download the XML file to see what can be filled out. Since this is a test submission, 
we will reduce that to the mandatory fields only, and we can copy some values from our previous bin sample submission.

You need to define an assembly quality here, Have a look at this FAQ:

https://ena-docs.readthedocs.io/en/latest/faq/metagenomes.html#how-is-the-quality-of-a-metagenomic-assembly-defined

The following is probably the correct quality value for our assembly:

"Multiple fragments where gaps span repetitive regions. Presence of the 23S, 16S and 5S rRNA genes and at least 18 tRNAs."

(and metagenome assemblies worse than that should probably not be submitted at all)

Again, you will also need to fill the taxon fields yourself. Look it up in the bin sample submission or have a look in the GTDBtk results again, look for your bin, and search the taxa in the NCBI taxonomy:
https://www.ncbi.nlm.nih.gov/taxonomy
Find out the taxid, common name and scientific name for your bin and fill the information in the XML file, also fill in completeness and contamination score from the CheckM results and the bin sample accession::

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
	        <TAG>assembly software</TAG>
		      <VALUE>MEGAHIT</VALUE>
	      </SAMPLE_ATTRIBUTE>
        <SAMPLE_ATTRIBUTE>
	        <TAG>completeness score</TAG>
		      <VALUE>TODO: fill in the completeness score of your MAG!</VALUE>
	      </SAMPLE_ATTRIBUTE>
        <SAMPLE_ATTRIBUTE>
	        <TAG>completeness software</TAG>
		      <VALUE>CheckM</VALUE>
	      </SAMPLE_ATTRIBUTE>
        <SAMPLE_ATTRIBUTE>
	        <TAG>contamination score</TAG>
		      <VALUE>TODO: fill in the contamination score of your MAG!</VALUE>
	      </SAMPLE_ATTRIBUTE>
        <SAMPLE_ATTRIBUTE>
	        <TAG>binning software</TAG>
		      <VALUE>METABAT</VALUE>
	      </SAMPLE_ATTRIBUTE>
        <SAMPLE_ATTRIBUTE>
	        <TAG>assembly quality</TAG>
		      <VALUE>Multiple fragments where gaps span repetitive regions. Presence of the 23S, 16S and 5S rRNA genes and at least 18 tRNAs.</VALUE>
	      </SAMPLE_ATTRIBUTE>
        <SAMPLE_ATTRIBUTE>
	        <TAG>binning parameters</TAG>
		      <VALUE>default</VALUE>
	      </SAMPLE_ATTRIBUTE> 
        <SAMPLE_ATTRIBUTE>
	        <TAG>taxonomic identity marker</TAG>
		      <VALUE>multi marker approach (GTDBtk)</VALUE>
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
		      <VALUE>TODO: you bin sample accession here!</VALUE>
	      </SAMPLE_ATTRIBUTE>
	      <SAMPLE_ATTRIBUTE>
		      <TAG>metagenomic source</TAG>
		      <VALUE>outdoor metagenome</VALUE>
	      </SAMPLE_ATTRIBUTE>
	    </SAMPLE_ATTRIBUTES>
	  </SAMPLE>
	</SAMPLE_SET>


Note that you would need to add one sample for each of the MAGs you would like to submit - and also register a locus tag prefix along with the study submission. In our case, as for the bins, we will only submit one bin for demonstration purposes.

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

Note your MAG sample accession number somewhere, you will need it for the next step.

Now, finally, it's time to submit the final result - our annotated MAG!


References
^^^^^^^^^^
**ENA - Submitting A Metagenome-Assembled Genome (MAG)** https://ena-docs.readthedocs.io/en/latest/submit/assembly/metagenome/mag.html

**ENA - Metagenome Submission Queries** https://ena-docs.readthedocs.io/en/latest/faq/metagenomes.html
