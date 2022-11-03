Submitting a bin sample
==================

There are two ways to submit a sample to ENA:

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
  
  TODO: CHANGE THAT
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

Get the correct ENA checklist
^^^^^^^^^^

...


Create sample.xml
^^^^^^^^^^

...

Submit the sample
^^^^^^^^^^^^^^^^

Now, it is time to submit::

  CHANGE THAT curl -u $ENA_USER:$ENA_PWD -F "SUBMISSION=@submission.xml" -F "PROJECT=@study.xml" "https://wwwdev.ebi.ac.uk/ena/submit/drop-box/submit/"

Make sure to use wwwdev to submit to the ENA test server.


References
^^^^^^^^^^
**ENA - Registering a Study** https://ena-docs.readthedocs.io/en/latest/submit/study.html
