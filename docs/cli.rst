Command Line Introduction: Excercises
=====================================

Excercise 1: Basic File Operations
----------------------------------

Tasks:
 1. Change to your home directory 
 2. Create a file named ‘test.txt’ (and check if it is there) 
 3. Create a directory named ‘tutorial’ 
 4. Copy ‘test.txt’ into the directory ‘tutorial’ 
 5. Delete ‘test.txt’ (in your home)  
 6. Change to ‘tutorial’ and rename ‘test.txt’ to ‘file.txt’ and verify 
 7. Remove the directory ‘tutorial’ and its contents 

Solution:

.. raw:: html

   <details>
   <pre>
   cd
   touch test.txt
   ls -lrt
   mkdir tutorial
   cp test.txt tutorial/ 
   rm test.txt
   cd tutorial
   mv test.txt file.txt
   ls
   rm file.txt
   cd ..
   rmdir tutorial
   </pre>
   </details>

Excercise 2: Links
------------------
Tasks:
 1. change to /mnt/ 
 2. Create a directory with the name “linux_intro” and give it to the user ubuntu 
 3. Go back to your home directory 
 4. Create a soft link called ‘linux_intro’ to /mnt/linux_intro

**Note:** this cannot be done using normal permission. Use sudo for operating with root privileges

Solution:

.. raw:: html

   <details>
   <pre>
   cd /mnt
   sudo mkdir linux_intro
   sudo chown ubuntu:ubuntu linux_intro
   cd
   ln -s /mnt/linux_intro
   </pre>
   </details>

Excercise 3: Display File Content
---------------------------------

Before you can do the next excercise, you need to donwload the
sequencing data:

::

   cd ~/linux_intro
   wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/linuxcourse/seqs.fasta

Tasks: 
 1. Use head and tail to inspect the file 
 2. Print the first and last entry of the fasta file to the command line 
 3. Browse the file using less, search for start codons

Solution:

.. raw:: html

   <details>
   <pre>
   head seqs.fasta
   tail seqs.fasta <br>
   head -n 2 seqs.fasta
   tail -n 2 seqs.fasta <br>
   less seqs.fasta   
   </pre>
   </details>

Excercise 4: Wildcards
----------------------

For the next excercise, we will donwload more sequencing data:

::

   wget https://openstack.cebitec.uni-bielefeld.de:8080/swift/v1/linuxcourse/linuxdata.tar.gz
   tar -zxvf linuxdata.tar.gz

Tasks:
 1. List all tools in /usr/local/bin/ starting with ‘blast’ 
 2. List all tools in /usr/local/bin/ starting with ‘blast’ followed by one additional character 
 3. List all tools in /usr/local/bin/ starting with ‘a’ or ‘b’ and ending with ‘c’ or ‘d’ 
 4. Copy all sequence files from the directory linuxdata to the linux_intro directory (except seqs.fasta)

Solution:

.. raw:: html

   <details>
   <pre>
   ls /usr/local/bin/blast* <br>
   ls /usr/local/bin/blast? <br>
   ls /usr/local/bin/[ab]*[cd] <br>
   cd ~/linux_intro
   cp ~/linuxdata/sequences* ~/linux_intro/
   cp ~/linuxdata/sequences_?.fasta ~/linux_intro/
   cp ~/linuxdata/sequences_[1-4].fasta ~/linux_intro/
   cp ~/linuxdata/sequences_{1..4}.fasta ~/linux_intro/
   </pre>
   </details>

Excercise 5: grep and wc
------------------------

Tasks: 
 1. Create a soft link to the Araport11_genes.gff from the previously uncompressed ‘linuxdata.tar.gz’-archive into your linux_intro
 2. Inspect the file using less 
 3. How many lines does the file contain?
 4. How many entries are there for Chromosome 1? 
 5. Find all entries related to ‘Auxin’ 
 6. Use the command “grep” to find a file inside the “linuxdata” directory that contains the words “Romeo and Juliet”

Solutoin:

.. raw:: html

   <details>
   <pre>
   cd ~/linux_intro
   cp ~/linuxdata/Araport11_genes.gff . 
   less Araport11_genes.gff 
   wc -l Araport11_genes.gff 
   grep -c "^Chr1" Araport11_genes.gff <br>
   grep Auxin Araport11_genes.gff <br>
   grep -r "Romeo und Juliet" ~/linuxdata/ 
   </pre>
   </details>

Excercise 6: Streams
--------------------

Tasks: 
 1. Use *cat* and wildcards to combine all sequence-files into a new file “sequences.fasta” 
 2. Use *head* and *tail* to get the *second* sequence from sequences.fasta 
 3. Use *grep* to store the sequence headers of sequences.fasta in a file 
 4. Use *grep*, *head* and *tail* to store headers 11-20 in a file 
 5. Append the headers 41-50 to the same (!) file 
 6. Also store the first 50 headers in a separate file. Do this in one command by using “tee” ! 
 7. Use *grep* and *wc* to find out the number of bases in sequences.fasta

Solutoin:

.. raw:: html

   <details>
   <pre>
   cat sequences_[1-4].fasta > sequences.fasta <br>
   head -n 4 | tail -n 2 sequences.fasta <br>
   grep ">" sequences.fasta > headers.txt 
   grep ">" sequences.fasta | head -n 20 | tail -n 10 > headers_2.txt 
   grep ">" sequences.fasta | head -n 50 | tail -n 10 >> headers_2.txt 
   grep ">" sequences.fasta | head -n 50 | tee headers50.txt | tail -n 10 >> headers_2.txt <br>
   grep -v ">" sequences.fasta | wc 
   </pre>
   </details>

Excercise 7: Tabular Data
-------------------------

Tasks: 
 1. How many features (CDS/mRNA/UTR…) are there for each type?
  **Hint:** features are in row 3, sort and uniq might be useful
 2. Create the same statistic for each chromosome 
  **Hint:** cut can select multiple columns 
 3. How many genes with a ‘kinase’ annotation are there per chromosome?

Solution:

.. raw:: html

   <details>
   <pre>
   cut -f 3 Araport11_genes.gff | sort | uniq -c | grep -v "#" <br>
   cut -f 1,3 Araport11_genes.gff | sort | uniq -c | grep -v "##" <br>
   grep kinase Araport11_genes.gff | cut -f 1,3 | grep gene | cut -f 1 | sort | uniq -c
   </pre>
   </details>
