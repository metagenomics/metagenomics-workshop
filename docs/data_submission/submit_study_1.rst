Submitting a study
==================

There are two ways to submit a study at ENA:

1) Using the Webinterface
-----------------------
The Webinterface for the dev submission database can be found at: https://wwwdev.ebi.ac.uk/ena/submit/webin/login
You could follow this guide: https://ena-docs.readthedocs.io/en/latest/submit/study/interactive.html

2) Registering a study programmatically
-----------------------
... using the linux command line tool ``curl``
We will use this approach in this short course. 

First, create a work folder for submissions and a subfolder for the study files::

mkdir -p /mnt/submission/study
cd /mnt/submission/study

Create submission.xml
^^^^^^^^^^
The next thing you need to to is to create a file submission.xml with the following content::

  <SUBMISSION>
     <ACTIONS>
        <ACTION>
           <ADD/>
        </ACTION>
        <ACTION>
           <HOLD HoldUntilDate="TODO: release date"/>
        </ACTION>
     </ACTIONS>
  </SUBMISSION>

You can use an editor like ``gedit`` to do so. Fill in a valid date like "2022-11-25". You might as well delete the complete ACTION block containing HOLD if the data should be released immediately. 

Create study.xml
^^^^^^^^^^
Now create file study.xml with the following content::

  <PROJECT_SET>
     <PROJECT alias="Your course alias here! Be creative">
        <TITLE>Test dataset from the de.NBI NFDI4Microbiota course on metagenomics 2022</TITLE>
        <DESCRIPTION>This is an artificial dataset that should contain 12 organisms.</DESCRIPTION>
        <SUBMISSION_PROJECT>
           <SEQUENCING_PROJECT/>
        </SUBMISSION_PROJECT>
     </PROJECT>
  </PROJECT_SET>

Again, use ``gedit``, ``vi`` or any other editor to create the file. Change the alias to something unique! You can also change title and description to your likings. 

It is possible to submit multiple studies at once, just add additional PROJECTs in the PROJECT_SET.

Submit the study
^^^^^^^^^^^^^^^^




References
^^^^^^^^^^
**ENA - Registering a Study** https://ena-docs.readthedocs.io/en/latest/submit/study.html
