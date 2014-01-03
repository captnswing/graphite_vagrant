# -*- mode: ruby -*-

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu-precise12042-x64-vbox43"
  config.vm.box_url = "http://box.puphpet.com/ubuntu-precise12042-x64-vbox43.box"
  #config.vm.box = "precise64"
  #config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.hostname = "graphite.example.com"

  config.vm.network "private_network", ip: "192.168.33.100"

  # use NFS for /vagrant folder, speed on built in folder sharing is very bad
  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  config.vm.provider "virtualbox" do |vbox|
    vbox.customize ["modifyvm", :id, "--name", "graphite"]
    vbox.customize ["modifyvm", :id, "--memory", 512]
    vbox.customize ["modifyvm", :id, "--cpuexecutioncap", 90]
    #vbox.customize ["modifyvm", :id, "--cpus", 2]
    #vbox.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.provision :chef_solo do |chef|
    #chef.log_level = :info
    chef.log_level = :debug
    chef.cookbooks_path = "provisioning/chef"
    chef.add_recipe "chef-graphite"
    #chef.add_recipe "chef-graphite::statsd"
  end

end
