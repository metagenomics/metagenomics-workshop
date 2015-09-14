Setting up your AWS instance
================================

As metagenome assemblies require a lot of compute resources, we will run the tutorial
on Amazon AWS. Each workshop participant will start an AWS instance and
run all jobs on this instance.

We will use the BiBiGrid framework to start an AWS instance. BiBiGrid is an automatic setup tool for the Oracle Grid Engine inside Amazon's Elastic Compute Cloud. It offers easy configurability and maintenance of a compute cluster of arbitrary size via command-line. See the `BiBiGrid home page <http://wiki.techfak.uni-bielefeld.de/bibiserv/BiBiGrid>`_ for more info.

First, download a special version of the BiBiGrid tool which you can use to start up an AWS instance which we pre-configured for this tutorial::

  mkdir ~/mg-tutorial
  cd ~/mg-tutorial
  wget https://s3-eu-west-1.amazonaws.com/mg-tutorial-adm/bibigrid_tutorial.tar.gz

Unzip the tar-ball and change to the bibigrid directory::

  tar xvzf bibigrid_tutorial.tar.gz
  cd bibigrid

Now you can start an AWS Instance::

  ./bibigrid.sh 

Once the AWS instance is running, make sure you take note of its IP address. BiBiGrid will give you the necessary information you need to login to the instance (note that in your case the IP address will be different!)::

  export BIBIGRID_MASTER=<AWS IP ADDRESS>

You can then log on the master node with::

  ssh -i MGAssemblyTutorial.pem ubuntu@$BIBIGRID_MASTER

