Setting up your OpenStack instance
==================================

As metagenome assemblies require a lot of compute resources, we will run the tutorial
in the CeBiTec OpenStack cloud. Each workshop participant will start an OpenStack instance and
run all jobs on this instance.

We will use the BiBiGrid framework to start an OpenStack instance. BiBiGrid
is a command line tool for the automated setup of HPC environments on OpenStack
or Amazon AWS cloud infrastructure. It offers easy configurability and maintenance
of an HPC compute cluster of arbitrary size via command-line. See the
`BiBiGrid home page
<https://wiki.cebitec.uni-bielefeld.de/bibiserv/index.php/BiBiGrid>`_ for more
info.

First, download a special version of the BiBiGrid tool which you can
use to start up an OpenStack instance which we pre-configured for this
tutorial::

  mkdir ~/mg-tutorial
  cd ~/mg-tutorial
  wget https://s3-eu-west-1.amazonaws.com/mg-tutorial-adm/bibigrid_tutorial.tar.gz

Unzip the tar-ball and change to the bibigrid directory::

  tar xvzf bibigrid_tutorial.tar.gz
  cd bibigrid

Edit the bibigrid.properties file and add (1) user name (2) password,
and (3) the path to your public SSH key for the OpenStack account
which was provided to you earlier in the course.

Now you can start an OpenStack Instance::

  ./bibigrid -c -o bibigrid.properties -u USERNAME

Once the OpenStack instance is running, make sure you **take note of its IP
address**. We will need it later!

BiBiGrid will give you the necessary information you need to
login to the instance (note that in your case the IP address will be
different!)::

  export BIBIGRID_MASTER=<OPENSTACK INSTANCE IP ADDRESS>

You can then log on the master node with::

  ssh -i PATH_TO_YOUR_SECRET_SSH_KEY_FILE ubuntu@$BIBIGRID_MASTER

