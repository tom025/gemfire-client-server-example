# Gemfire client server example

The intention is to provide a working example of a non trivial
[gemfire](https://pivotal.io/pivotal-gemfire) client-server setup working with
[spring boot](https://projects.spring.io/spring-boot/).

I hope to demonstrate:

  * Provisioning of servers hosting gemfire in a repeatable way.
  * Configuring of gemfire locators and cache-servers into a cluster.
  * Configuring of cache-clients that connect to the cluster.
  * Deploying code, such as functions, to gemfire.

## Provisioning servers

### Bootstrapping a development environment

This project uses ansible to provision gemfire servers that are hosted using
VirtualBox via vagrant for automation. You will need to bootstrap your
development environment with 

    $ ./bootstrap

This script assumes that the development environment being bootstrapped is
running OS X which has recent version of [homebrew](https://brew.sh/)
installed. In the future it would be desirable for other platforms to be
supported by this script.

The `./bootstrap` script will ensure that the following software is installed:
    * [Vagrant](https://www.vagrantup.com/) - Used for managing VMs with
      VirtualBox
    * [Landrush](https://github.com/vagrant-landrush/landrush) - A Vagrant
      plugin that manages DNS records for Vagrant managed VMs.
    * [Python](https://www.python.org/) - The programming language that Ansible
      is build with.
    * [virtualenv](https://pypi.python.org/pypi/virtualenv) - A python package
      for isolating python environments.
    * [Ansible](https://www.ansible.com/) - Used for automated provisioning of
      services.

All the ansible binaries will be installed to `.ansible_virtualenv/bin`.
You should add this directory to your `$PATH`.

    $ export PATH=.ansible_virtualenv/bin:$PATH

If you are using [direnv](https://direnv.net/) then ansible will automatically
be added to your path when changing to the project directory.

### Starting services with Vagrant

Use the `vagrant` command to download the VMs and start them. This can be
achieved by running:

    $ vagrant up

You may want to test that you can reach the machine by running:

    $ vagrant ssh

You should see a prompt like:

    ubuntu@gemfire-locator:~$

You may want to test that DNS resolution is working as well by running:

    $ nslookup gemfire-locator.gemfire-example.dev

You should see an output similar to:

		Server:		172.20.10.1
		Address:	172.20.10.1#53

		Non-authoritative answer:
		Name:	gemfire-locator.gemfire-example.dev
		Address: 127.0.53.53

Everything should now be setup for provisioning the VMs with gemfire.

### Provisioning servers with gemfire

To provision everything run

    $ ./provision

This will run ansible provisioning scripts on the vagrant hosts.
