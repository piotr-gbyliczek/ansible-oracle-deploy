# -*- mode: ruby -*-
# vi: set ft=ruby :

file_to_disk = '.vagrant/large_disk.vdi'
file_to_disk1 = '.vagrant/disk1.vdi'
file_to_disk2 = '.vagrant/disk2.vdi'
file_to_disk3 = '.vagrant/disk3.vdi'
file_to_disk4 = '.vagrant/disk4.vdi'

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
     controller = 'SCSI'
     vb.customize ["storagectl", :id, "--name", "#{controller}", "--add", "scsi"]
     unless File.exist?(file_to_disk)
       vb.customize ['createhd', '--filename', file_to_disk, '--size', 100 * 1024]
     end
     vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 0, '--device', 1, '--type', 'hdd', '--medium', file_to_disk]
     unless File.exist?(file_to_disk1)
       vb.customize ['createhd', '--filename', file_to_disk1, '--size', 10 * 1024]
     end
     vb.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 0, '--device', 0, '--type', 'hdd', '--medium', file_to_disk1]
     unless File.exist?(file_to_disk2)
       vb.customize ['createhd', '--filename', file_to_disk2, '--size', 10 * 1024]
     end
     vb.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', file_to_disk2]
     unless File.exist?(file_to_disk3)
       vb.customize ['createhd', '--filename', file_to_disk3, '--size', 5 * 1024]
     end
     vb.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', file_to_disk3]
     unless File.exist?(file_to_disk4)
       vb.customize ['createhd', '--filename', file_to_disk4, '--size', 5 * 1024]
     end
     vb.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', file_to_disk4]
  end
  config.vm.provision :ansible do |ansible|
#    ansible.verbose = "vvvv"
#    ansible.limit = "all"
    ansible.playbook = "deploy.yml"
#    ansible.tags = "initial_run"
  end
end




