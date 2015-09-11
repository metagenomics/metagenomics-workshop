Setting up your AWS instance
================================

As metagenome assemblies require a lot of compute resources, we will run the tutorial
on Amazon AWS. Each workshop participant will start an AWS instance and
run all jobs on this instance.

First, download the BiBiGrid tool which you can use to easily start up a pre-configured
AWS instance::

  wget http://somewhere/bibigrid_tutorial.tar.gz

Unzip the tar-ball and change to the bibigrid directory::

  tar xvzf bibigrid_tutorial.tar.gz
  cd bibigrid

Now you can start an AWS Instance::

  ./bibigrid.sh 


