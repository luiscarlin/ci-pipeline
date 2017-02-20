
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
BASE_HOSTNAME = "vagrant"
BASE_IP = "192.168.0."
NUM_MACHINES = 2

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  (1..NUM_MACHINES).each do |id|
    config.vm.define "#{BASE_HOSTNAME}#{id}" do |machine|
      machine.vm.box = "centos/7"
      machine.vm.hostname = "#{BASE_HOSTNAME}#{id}"
      machine.vm.network "private_network", ip: "#{BASE_IP}#{10+id}"

      machine.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--name", "#{BASE_HOSTNAME}#{id}"]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
        v.customize ["modifyvm", :id, "--cpus", 1]
      end

      machine.ssh.insert_key = false

      if id == NUM_MACHINES
        machine.vm.provision :ansible do |ansible|
          ansible.verbose = "v"
          ansible.limit = "all"
          ansible.playbook = "main.yml"
          ansible.inventory_path = "inventories/hosts"
          ansible.sudo = true
        end

        machine.vm.provision :shell, inline: "echo Finsihed"
      end
    end
  end
end
