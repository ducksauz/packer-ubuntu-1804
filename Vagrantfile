# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', type: 'nfs'

  # VMware Fusion.
  # `vagrant up vmware --provider=vmware`
  config.vm.define "vmware" do |vmware|
    vmware.vm.hostname = "ubuntu1804-vmware"
    vmware.vm.box = "file://builds/vmware-ubuntu1804.box"
    vmware.vm.network :private_network, ip: "192.168.3.2"

    config.vm.provider :vmware_desktop do |v, override|
      v.gui = false
      v.vmx["memsize"] = 1024
      v.vmx["numvcpus"] = 1
      v.vmx["ethernet0.pcislotnumber"] = "33"
    end

    config.vm.provision "shell", inline: "echo Hello, World"
  end

  # VirtualBox.
  config.vm.define "virtualbox" do |virtualbox|
    virtualbox.vm.hostname = "virtualbox-ubuntu1804"
    virtualbox.vm.box = "file://builds/virtualbox-ubuntu1804.box"
    virtualbox.vm.network :private_network, ip: "172.16.3.2"

    config.vm.provider :virtualbox do |v|
      v.gui = false
      v.memory = 1024
      v.cpus = 1
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    config.vm.provision "shell", inline: "echo Hello, World"
  end

end
