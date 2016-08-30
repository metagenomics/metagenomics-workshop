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
  cp -r /vol/metagencourse/bibigrid/ .

Change to the bibigrid directory::

  cd ~/mg-tutorial/bibigrid

Edit the bibigrid.properties file and 

1. add user name
2. add password
3. add path to your public SSH key for the OpenStack account

Change file permissions for .properties file::

  chmod go-rwx bibigrid.properties

Now you can start an OpenStack Instance::

  ./bibigrid.sh -c -o bibigrid.properties -u USERNAME

Once the OpenStack instance is running, make sure you **take note of its IP
address**. We will need it later!

BiBiGrid will give you the necessary information you need to
login to the instance (note that in your case the IP address will be
different!)::

  export BIBIGRID_MASTER=<OPENSTACK INSTANCE IP ADDRESS>

You can then log on the master node with::

  ssh -i PATH_TO_YOUR_SECRET_SSH_KEY_FILE ubuntu@$BIBIGRID_MASTER

