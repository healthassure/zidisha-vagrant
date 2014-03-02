# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "saucy-64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.hostname = "zidisha-dev"
  config.ssh.forward_agent = true
  config.ssh.port = 2225
  config.vm.network :forwarded_port, guest: 22, host: 2225, id:'ssh'
  config.vm.network :private_network, ip: "192.168.90.103"
  config.vm.synced_folder "shared", "/workspace"

  config.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
  end

  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.verbose = "vvvv"
      ansible.inventory_path = "provisioning/hosts"
  end
end
