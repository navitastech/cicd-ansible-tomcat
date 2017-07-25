# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version.
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "vagrant"

  config.vm.network "forwarded_port", guest: 8080, host: 11700
  config.vm.network "forwarded_port", guest: 11300, host: 11300

  config.vm.hostname = "localhost"

  config.vm.box = "centos/7"
  config.vm.box_check_update = false
 

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    v.memory = 8192
  end

  ansible_groups = {
      "local" => ["vagrant"]
  }

  config.vm.provision "ansible" do |ansible|
      ansible.verbose  = "vvvv"
      ansible.groups   = ansible_groups
      ansible.playbook = "provision-app.yml"

  end
end
