# -*- mode: ruby -*-
# vi: set ft=ruby :

file_to_disk = '.vagrant/large_disk.vdi'

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.landrush.enabled = true
  config.landrush.host_redirect_dns = false
  config.landrush.tld = 'oss.node4.co.uk'
  config.vm.hostname = "oracledeploy.#{config.landrush.tld}"
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.121.10"
  config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
     vb.cpus = 2
     vb.memory = "1024"
     vb.customize ['createhd', '--filename', file_to_disk, '--size', 500 * 1024]
     vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 0, '--device', 1, '--type', 'hdd', '--medium', file_to_disk]
  end
  config.vm.provision :ansible do |ansible|
#    ansible.verbose = "vvvv"
#    ansible.limit = "all"
    ansible.playbook = "deploy.yml"
#    ansible.tags = "initial_run"
  end
end




