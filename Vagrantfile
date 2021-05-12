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

cluster = {
  "master1" => { :ip => "192.168.50.10", :cpus => 2, :mem => 2048 },
  #{}"master2" => { :ip => "192.168.50.13", :cpus => 1, :mem => 1024 },
  #{}"master3" => { :ip => "192.168.50.14", :cpus => 1, :mem => 1024 },
  "node1" => { :ip => "192.168.50.11", :cpus => 1, :mem => 1024 },
  "node2" => { :ip => "192.168.50.12", :cpus => 1, :mem => 1024 }
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = VAGRANT_BOX

  cluster.each_with_index do |(hostname, info), index|

    config.vm.define hostname do |cfg|
      cfg.vm.provider :virtualbox do |vb, override|
        override.vm.network :private_network, ip: "#{info[:ip]}"
        override.vm.hostname = hostname + ".local"
        vb.name = hostname
        vb.customize ["modifyvm", :id, "--memory", info[:mem], "--cpus", info[:cpus]]
      end # end provider
    end # end config
  end # end cluster
  # Sync folder
  config.vm.synced_folder HOST_PATH, GUEST_PATH
  # Disable default Vagrant folder, use a unique path per project
  config.vm.synced_folder '.', '/home/'+VM_USER+'', disabled: true

  # Just uncomment this part to provision the Environment hier with Vagrant
  #config.vm.provision "ansible" do |ansible|
  #  ansible.playbook = "playbook.yml"
  #  ansible.inventory_path= "./inventory"
  #end
end
