.. note:: Most jobs above will be started on the compute cluster using the ``qsub``.

   * ``qstat``:  check the status and JOBNUMBER of your jobs
   * ``qdel JOBNUMBER``: delete job with job number JOBNUMBER
  
 We usually submit the jobs to the cluster giving them a job name by using ``-N JOBNAME``.
 This will create log-files named 
  
   * ``JOBNAME.oJOBNUMBER``: standard output messages of the tool
   * ``JOBNAME.eJOBNUMBER``: standard error messages of the tool
  
 You can look into these files by typing e.g. ``less JOBNAME.oJOBNUMBER`` (hit ``q`` to quit) 
 or ``tail -f JOBNAME.oJOBNUMBER`` (hit ``^C`` to quit).


