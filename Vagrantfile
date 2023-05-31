# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.synced_folder "./data", "/opt/mastodoncio", create: true

  config.vm.define "vps" do |vps|
    vps.vm.box = "ubuntu/lunar64"
    vps.vm.hostname = "mastodon-vagrant-docker"
    vps.vm.network "forwarded_port", guest: 9090, host: 9090
    vps.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 4
      v.default_nic_type = "virtio"
      v.customize ["modifyvm", :id, "--natnet1", "10.254.0.0/16"]
    end

    vps.vm.provision "ansible", playbook: "ansible/101-dependencias.yml"
    vps.vm.provision "ansible", playbook: "ansible/102-podman.yml"
    vps.vm.provision "ansible", playbook: "ansible/103-openvpn.yml"
  end
end
