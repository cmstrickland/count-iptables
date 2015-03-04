# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"



Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "debian-testing-base"
  config.vm.hostname = "iptables-vm"

  # ip address is convigurable via environment variable
  ipaddr = ENV['IPTABLES_VM_IP'] || "192.168.100.105"
  config.vm.network "private_network", ip: ipaddr

  # use ansible provisioning to apply configuration to base box
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "iptables.yml"
  end
end
