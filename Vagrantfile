# -*- mode: ruby -*-

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu-precise12042-x64-vbox43"
  config.vm.box_url = "http://box.puphpet.com/ubuntu-precise12042-x64-vbox43.box"
  #config.vm.box = "precise64"
  #config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.hostname = "graphite.example.com"

  # carbon
  config.vm.network "forwarded_port", guest: 2003, host: 2003
  # graphite gui
  config.vm.network "forwarded_port", guest: 8085, host: 8085
  # statsd
  #config.vm.network "forwarded_port", guest: 8125, host: 8125

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
