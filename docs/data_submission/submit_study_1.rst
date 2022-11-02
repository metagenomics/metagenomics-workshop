Submitting a study
==================

There are two ways to submit a study at ENA:

1) Using the Webinterface at https://wwwdev.ebi.ac.uk/ena/submit/webin/login
You could follow this guide: https://ena-docs.readthedocs.io/en/latest/submit/study/interactive.html

2) Registering a study programmatically using the linux command line tool ``curl``
We will use this approach in this short course. 

First, create a work folder for submissions and a subfolder for the study files::

mkdir -p /mnt/submission/study
cd /mnt/submission/study

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


References
^^^^^^^^^^
**ENA - Registering a Study** https://ena-docs.readthedocs.io/en/latest/submit/study.html
