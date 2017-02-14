## files: Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :
hosts = {
  "node1" => "192.168.0.11",
  "node2" => "192.168.0.12",
  "node3" => "192.168.0.13",
  "node4" => "192.168.0.14",
  "node5" => "192.168.0.15"
}

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.2"
  config.vm.box_url = "./vagrant-centos-7.2.box"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm",:id,"--memory",512]
  end
  hosts.each do |name, ip|
    config.vm.define name do |nodes|
      nodes.vm.hostname = name
      nodes.vm.network :private_network, ip: ip
      nodes.vm.synced_folder ".","/vagrant", disabled: true
      nodes.vm.provision "shell",
        run: "always",
        inline: "sudo ifup enp0s8"
      end
    end
  end
