Data submission to ENA - Intro
======================

We will submit our analysis to ENA now. We will use the ENA dev/test Server for all submissions. Submissions sent there will be deleted every night, so it is a good environment for all kind of tests regarding submissions.

Structure of this lesson
^^^^^^^^^^^^^^^^^^

The aim of this lesson is to submit everything we generated so far: raw data, assembly, binning and MAGs. To reduce the amount of work, we will submit one bin/MAG after the submission of assemblies. The complete submission will work in the following order:

1. Create a study 
2. Create a sample
3. Submit raw reads
4. Submit the assembly results
5. Create a sample for the selected bin we want to submit
6. Submit the bin
7. Create a sample for the selected MAG we want to submit
8. Submit the MAG (do the annotation with prokka before doing that)

So there is a lot to be done. Let's get started by getting webin-cli - a command line tool provided by ENA to allow/facilitate some submissions on the command line

Getting webin-cli
^^^^^^^^^^^^^^^^

Getting webin-cli is easy - just get the latest jar from this git repository:

https://github.com/enasequence/webin-cli/

As of today, the latest version is 6.10.0, get it using ``wget``::

  cd
  https://github.com/enasequence/webin-cli/releases/download/6.10.0/webin-cli-6.10.0.jar
  
If you want, you can read the help message with::

  java -jar ~webin-cli-6.10.0.jar -help
  
We will need that tool in later steps. Study and sample will be created in the web interface and bin samples will be submitted using ``curl``.


Set credentials as environment variables
^^^^^^^^^^^^^^^^

To not type your username password every time you submit, you should store them as environment variables::

  export ENA_USER=Webin-xxxx
  export ENA_PWD=password

This will allow you, to just copy and paste the submit commands in this documentation.
