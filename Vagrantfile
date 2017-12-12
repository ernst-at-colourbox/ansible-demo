# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos/7"
  # config.vm.box = "mvbcoding/awslinux"

  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 3
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  
  N = 4
  (1..N).each do |machine_id|
    config.vm.define "machine#{machine_id}" do |machine|
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", type: "dhcp"
      
      # Only execute once the Ansible provisioner,
      # when all the machines are up and ready.
      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          ansible.groups = {
            "web" => ["machine1", "machine2"],
            "db"  => ["machine3"],
            "lb"  => ["machine4"]
          }          
          # Disable default limit to connect to all the machines
          ansible.limit = "all"      
          ansible.playbook = "misc/vagrant-playbook.yml"
        end
      end
    end
  end
end
