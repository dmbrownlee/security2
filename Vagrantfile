# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.ssh.private_key_path= "../keys/vagrant"
  # Common to all VMs
  config.vm.box = "ubuntu-16.04.1-desktop-amd64"
  config.vm.boot_timeout = 60
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provision :ansible do |ansible|
    ansible.verbose = "vv"
    ansible.playbook = "ansible/vagrant-vm-playbook.yml"
  end

  # SecurityOnion
  config.vm.define "SecurityOnion" do |node|
    node.vm.hostname = "SecurityOnion"
    node.vm.box = "ubuntu-14.04.5-desktop-amd64"
    node.vm.network "private_network", ip: "192.168.201.253", virtualbox__intnet: "net1", auto_config: false
    node.vm.synced_folder "data/", "/data"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "SecurityOnion"
      vb.memory = 2048
      vb.cpus = 2
      vb.customize ["modifyvm", :id, "--vrde", "off"]
      vb.customize ["modifyvm", :id, "--vram", "128"]
      vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
      vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    end
  end

  # First Ubuntu desktop
  config.vm.define "pc-192.168.201.100" do |node|
    node.vm.hostname = "pc-192-168-201-100"
    node.vm.network "private_network", ip: "192.168.201.100", virtualbox__intnet: "net1", auto_config: false
    node.vm.synced_folder "data/", "/data"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "pc-192.168.201.100"
      vb.customize ["modifyvm", :id, "--vrde", "off"]
      vb.customize ["modifyvm", :id, "--vram", "128"]
      vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
    end
  end

  # Second Ubuntu desktop
  config.vm.define "pc-192.168.201.101" do |node|
    node.vm.hostname = "pc-192-168-201-101"
    node.vm.network "private_network", ip: "192.168.201.101", virtualbox__intnet: "net1", auto_config: false
    node.vm.synced_folder "data/", "/data"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "pc-192.168.201.101"
      vb.customize ["modifyvm", :id, "--vrde", "off"]
      vb.customize ["modifyvm", :id, "--vram", "128"]
      vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
    end
  end

  # Kali
  config.vm.define "Kali-Linux-2016.2" do |node|
    node.vm.box = "Kali-Linux-2016.2"
    #node.vm.hostname = "Kali-Linux-2016.2"
    node.vm.network "private_network", ip: "192.168.201.103", virtualbox__intnet: "net1", auto_config: false
    node.vm.synced_folder "data/", "/data"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "Kali-Linux-2016.2"
      vb.customize ["modifyvm", :id, "--vrde", "off"]
      vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-vms"]
    end
  end

  # Metasploitable2
  config.vm.define "Metasploitable2" do |node|
    node.vm.box = "Metasploitable2"
    node.vm.hostname = "Metasploitable2"
    node.vm.network "private_network", ip: "192.168.201.102", virtualbox__intnet: "net1", auto_config: false
    node.vm.provider "virtualbox" do |vb|
      vb.name = "Metasploitable2"
      vb.customize ["modifyvm", :id, "--vrde", "off"]
    end
  end
end
