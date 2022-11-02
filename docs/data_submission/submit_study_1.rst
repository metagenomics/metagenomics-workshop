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
     <PROJECT alias="cheddar_cheese">
        <TITLE>Characterisation of Microbial Diversity and Chemical Properties of Cheddar Cheese Prepared from Heat-treated Milk</TITLE>
        <DESCRIPTION>This study aimed to characterise the interaction of microbial diversity and chemical properties of Cheddar cheese after three different heat treatments of milk</DESCRIPTION>
        <SUBMISSION_PROJECT>
           <SEQUENCING_PROJECT/>
        </SUBMISSION_PROJECT>
     </PROJECT>
  </PROJECT_SET>

You can submit multiple 
You can use an editor like ``gedit`` to do so. Fill in a valid date like "2022-11-25". You might as well delete the complete ACTION block containing HOLD if the data should be released immediately. 


References
^^^^^^^^^^
**ENA - Registering a Study** https://ena-docs.readthedocs.io/en/latest/submit/study.html
