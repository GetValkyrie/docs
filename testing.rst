Continuous Integration
======================

We use Jenkins as the basis of our Continuous Integration system.


Vagrant
-------

We currently use AWS EC2, provisioned using the Vagrant AWS plugin, as our
principle testing platform. We should be able to easily provision full test
stacks locally, or on any other supported cloud platforms with a minimum of
modification to the general framework.

Vagrant allows us to configure servers using a number provisioning options.
While we prefer Puppet_ for production environments, for immutable_ utility
servers and prototyping, shell scripts work quite well.

First you install Vagrant from the upstream ``.deb`` files because the
Debian ones are not up to date enough::

  wget https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.3_x86_64.deb
  sudo dpkg -i vagrant_1.6.3_x86_64.deb

The latest version may vary of course, since this was written, look at
the `download page <http://www.vagrantup.com/downloads.html>`_ for the
latest version. You will also need a Virtualbox install::

  sudo apt-get install virtualbox

The next step is to fetch the Vagrant/Puppet code from git::

  git clone https://github.com/GetValkyrie/anthology

Then you're ready to setup vagrant hosts, for example to setup ``gitlab``::

  cd anthology
  vagrant up gitlab

.. todo::
  Research Ansible, which appears to be quite straight-forward, in comparison
  to Puppet, and is configured using YAML.

.. _Puppet: http://puppetlabs.com
.. _immutable: http://martinfowler.com/bliki/ImmutableServer.html


EC2 AMI
-------

Since we're building test servers, we'll often prefer to stick with t2.micro
instances, as they fall within 'free tier'. Unfortunately, only HVM AMIs are
available for t2.micro instances, so we'll need to use that AMI (ami-a6d611ce).

For further details, see the docs for our :ref:`EC2-AMIs-label`.


Jenkins
-------

We install and configure Jenkins using a shell script. It basically adds the
Jenkins Debian repo and its key, installs the latest Jenkins, along with
jenkins-job-builder. It then disables unused plugins.

.. todo:: install useful plugins
.. todo:: install jenkins-cli
.. todo:: configure jjb
.. todo:: create jjb repo for jobs
.. todo:: manage jenkins users/config directly in repo



