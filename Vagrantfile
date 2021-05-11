# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# Box / OS
VAGRANT_BOX = 'centos/7'

# VM User — 'vagrant' by default
VM_USER = 'nomad'

# Username on your Mac
#MAC_USER = 'John'

# Host folder to sync
HOST_PATH = './jobs'

# Where to sync to on Guest — 'vagrant' is the default user name
GUEST_PATH = '/vagrant'

# # VM Port — uncomment this to use NAT instead of DHCP
# VM_PORT = 8080

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Vagrant box from Hashicorp
  config.vm.box = VAGRANT_BOX

  # Set VM name in Virtualbox
  config.vm.define :master1 do |master1|
    master1.vm.hostname = "master1.local"
    master1.vm.network "private_network", ip: "192.168.50.10"
    master1.vm.provider :virtualbox do |vb|
      vb.name = "master1"
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
    end
    #master1.vm.provision "docker"
    master1.vm.provision :hosts do |provisioner|
        provisioner.add_host '192.168.50.10', ['master1.local']
        provisioner.add_host '192.168.50.11', ['node1.local']
        provisioner.add_host '192.168.50.12', ['node2.local']
    end
  end

  config.vm.define :node1 do |node1|
    node1.vm.hostname = "node1.local"
    node1.vm.network "private_network", ip: "192.168.50.11"
    node1.vm.provider :virtualbox do |vb|
      vb.name = "node1"
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
    end
    #node1.vm.provision "docker"
    node1.vm.provision :hosts do |provisioner|
        provisioner.add_host '192.168.50.10', ['master1.local']
        provisioner.add_host '192.168.50.11', ['node1.local']
        provisioner.add_host '192.168.50.12', ['node2.local']
    end
  end

  config.vm.define :node2 do |node2|
    node2.vm.hostname = "node2.local"
    node2.vm.network "private_network", ip: "192.168.50.12"
    node2.vm.provider :virtualbox do |vb|
      vb.name = "node2"
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
    end
    #node2.vm.provision "docker"
    node2.vm.provision :hosts do |provisioner|
        provisioner.add_host '192.168.50.10', ['master1.local']
        provisioner.add_host '192.168.50.11', ['node1.local']
        provisioner.add_host '192.168.50.12', ['node2.local']
    end
  end


  #DHCP — comment this out if planning on using NAT instead
  #config.vm.network "private_network", type: "dhcp"
  # # Port forwarding — uncomment this to use NAT instead of DHCP
  # config.vm.network "forwarded_port", guest: 80, host: VM_PORT
  # Sync folder
  config.vm.synced_folder HOST_PATH, GUEST_PATH
  # Disable default Vagrant folder, use a unique path per project
  config.vm.synced_folder '.', '/home/'+VM_USER+'', disabled: true
end
