Quality Treatment
====================================================
In this excercise you will learn how to quality trim Illumina paired-end reads.
Illumna paired-end reads are still the most common NGS approach for metagenomics.

We will now use some reads that show some issues regarding the data quality. 
First of all, lets have a look on some real sequencing data::

  mkdir -p /mnt/qc
  cd /mnt/qc
  wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/mgcourse_data/qc.tgz
  tar -xvzf qc.tgz
  fastqc *.fastq
  
Let's again inspect the results ...

Run fastp on a PE library
======================================
For quality trimming we use the software fastp which trims reads from 5' end to 3' end using a sliding window.
If the mean quality of bases inside a window drops below a specific q-score, the remaining of the read will be trimmed.
If a read get too short during this trimming, it will be discared. 

First, call the hel ppage for fastp and inspect all parameters, then run fastp::

	fastp \
	        -i forward.fastq \
	        -I reverse.fastq \
	        -o forward_qc1.fastq \
          	-O reverse_qc1.fastq \						
		--cut_tail -Q -A -G -w 16

Let's again inspect the results. Now compare the effect with the untrimmed reads::

  fastqc forward_qc1.fastq reverse_qc1.fastq

Run FastP again
================
Still, the reads show some issues on the 3' end. We will try ti get rid of the poly-G tail::

	fastp \
	        -i forward.fastq \
	        -I reverse.fastq \
	        -o forward_qc2.fastq \
          	-O reverse_qc2.fastq \						
		--cut_tail -A -g --poly_g_min_len 5 -w 16

And again inspect the results using fastqc::

  fastqc forward_qc2.fastq reverse_qc2.fastq


Trimming adapter sequence
=========================

The FastQC report still shows some adapter contamination. We can use FastP also for this, but other tolls have shown to perform better performance on this task.
Thus, we will use cutadapt for this. But first we need to identify the primers and adapters that were used. Usually, this should be communicated with your sequencing facility.
For this data, we can have a look on the following websites:

https://dnatech.genomecenter.ucdavis.edu/wp-content/uploads/2019/03/illumina-adapter-sequences-2019-1000000002694-10.pdf
https://teichlab.github.io/scg_lib_structs/methods_html/Illumina.html

So the sequence that needs to be trimmed off from our reads are::

  forward: CTGTCTCTTATACACATCT
  reverse: CTGTCTCTTATACACATCT
  
We can the feed these into cutdapt to trim the 3' ends of the reads::

  #-f fastq does not work? remove?
  cutadapt -e 0.15 -O 10 -m 25 \
  	-a CTGTCTCTTATACACATCT \
  	-A CTGTCTCTTATACACATCT\
  	-o forward_qc3.fastq -p reverse_qc3.fastq \
  	forward_qc2.fastq reverse_qc2.fastq

Finally, we will unce fastqc once again to see if we solved the issue::

  fastqc forward_qc3.fastq reverse_qc3.fastq

