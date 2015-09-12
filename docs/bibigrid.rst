Setting up your AWS instance
================================

As metagenome assemblies require a lot of compute resources, we will run the tutorial
on Amazon AWS. Each workshop participant will start an AWS instance and
run all jobs on this instance.

We will use the BiBiGrid framework to start an AWS instance. BiBiGrid is an automatic setup tool for the Oracle Grid Engine inside Amazon's Elastic Compute Cloud. It offers easy configurability and maintenance of a compute cluster of arbitrary size via command-line. See the `BiBiGrid home page <http://wiki.techfak.uni-bielefeld.de/bibiserv/BiBiGrid>`_ for more info.

First, download a special version of the BiBiGrid tool which you can use to start up an AWS instance which we pre-configured for this tutorial::

  wget http://somewhere/bibigrid_tutorial.tar.gz

Unzip the tar-ball and change to the bibigrid directory::

  tar xvzf bibigrid_tutorial.tar.gz
  cd bibigrid

Now you can start an AWS Instance::

  ./bibigrid.sh 


