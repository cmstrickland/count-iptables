# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

# this vagrant file will provision a working installation of wrangler
# using ansible, and the playbook manifests found in ./provisioning

# the VM has a NAT ethernet interface, and a private network which binds
# to 192.168.100.100 by default, but can be configured to use a different
# address by setting the WVM_IP environment variable to an IP address

# the VM will try to use NFS sharing to mount CWD as /vagrant for
# better performance. This will require an admin user password entry
# on vagrant startup. This shouldn't be a problem for Macs. You can
# revert to using virtualbox native sharing for /vagrant by setting
# WVM_NO_NFS in the environment, but this results in reduced
# performance as the app is very IO bound in developer mode

# to boot the box with defaults , just 'vagrant up' if there is a
# problem with the provisioning, you can retry with 'vagrant provision'

# example custom options invocation, setting an IP and disabling NFS
# 'WVM_NO_NFS=1 WVM_IP=10.0.0.4 vagrant up'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "debian-testing-base"
  config.vm.hostname = "iptables-vm"

  # ip address is convigurable via environment variable
  ipaddr = ENV['WVM_IP'] || "192.168.100.105"
  config.vm.network "private_network", ip: ipaddr

  # use ansible provisioning to apply configuration to base box
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "iptables.yml"
  end
end
