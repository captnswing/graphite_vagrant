require 'berkshelf/vagrant'

Vagrant::Config.run do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  #config.vm.forward_port "gunicorn", 8000, 8787
  #config.vm.forward_port "graphite-dev", 8080, 8888

  config.vm.provision :chef_solo do |chef|
    chef.log_level = :info
    chef.add_recipe "chef-graphite"
  end

end
