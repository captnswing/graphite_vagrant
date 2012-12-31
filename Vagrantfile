require 'berkshelf/vagrant'

Vagrant::Config.run do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.host_name = "graphite.vagrant"
  config.vm.customize ["modifyvm", :id, "--memory", 512]
  #config.vm.customize ["modifyvm", :id, "--cpus", 2 ]

  # carbon
  config.vm.forward_port 2003, 2003
  # graphite gui
  config.vm.forward_port 8085, 8085
  # statsd
  #config.vm.forward_port 8125, 8125

  config.vm.provision :chef_solo do |chef|
    chef.log_level = :info
    #chef.log_level = :debug
    chef.add_recipe "chef-graphite"
    #chef.add_recipe "chef-graphite::statsd"
  end

end
