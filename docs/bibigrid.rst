Setting up your OpenStack instance
==================================

As metagenome assemblies require a lot of compute resources, we will run the tutorial
in the de.NBI OpenStack cloud. Each workshop participant will start an two OpenStack instances 
and run all jobs on these instances.

We will use the BiBiGrid framework to start the OpenStack instances. BiBiGrid
is a command line tool for the automated setup of HPC environments on OpenStack, Amazon AWS 
or Google Compute Platform cloud infrastructure. It offers easy configurability and maintenance
of an HPC compute cluster of arbitrary size via command-line. See the
`BiBiGrid github page <https://github.com/BiBiServ/bibigrid>`_ for more info.

First, download a special version of the BiBiGrid tool which you can
use to start up an OpenStack instance which we pre-configured for this
tutorial::

  mkdir ~/mg-tutorial
  cd ~/mg-tutorial
  cp -r /vol/metagencourse/bibigrid/ .

Change to the bibigrid directory::

  cd ~/mg-tutorial/bibigrid

Edit the bibigrid.yml file and 

1. add ELIXIR username
2. add Openstack password
3. add path to your SSH key file for the OpenStack account
4. add name of OpenStack SSH key

Change file permissions for bibigrid.yml file::

  chmod go-rwx bibigrid.yml

Now you can start an OpenStack Instance::

  java -jar bibigrid-openstack-2.0.jar -o bibigrid.yml -c

Once the OpenStack instance is running, make sure you **take note of its IP
address**. We will need it later!

BiBiGrid will give you the necessary information you need to
login to the instance (note that in your case the IP address will be
different!)::

  export BIBIGRID_MASTER=<OPENSTACK INSTANCE IP ADDRESS>

You can then log on the master node with::

  ssh -i PATH_TO_YOUR_SECRET_SSH_KEY_FILE ubuntu@$BIBIGRID_MASTER

