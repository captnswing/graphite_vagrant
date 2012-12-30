# graphite-vagrant

### Summary, what is this?

* a [Vagrantfile](http://vagrantup.com/v1/docs/vagrantfile.html) to install [graphite](http://graphite.wikidot.org) into a virtual linux box
* using a [chef cookbook](http://docs.opscode.com/essentials_cookbooks.html) for graphite that [I've written](https://github.com/captnswing/chef-graphite)


### What do you need to get this going?

###### virtualbox

    curl -O http://dlc.sun.com.edgesuite.net/virtualbox/4.2.6/VirtualBox-4.2.6-82870-OSX.dmg
    hdid VirtualBox-4.2.6-82870-OSX.dmg
    sudo installer -target '/' -pkg /Volumes/VirtualBox/VirtualBox.pkg
    diskutil eject /Volumes/VirtualBox; rm VirtualBox-4.2.6-82870-OSX.dmg

###### ruby 1.9.3

    curl -L https://get.rvm.io | bash -s stable --ruby
    rvm --default use 1.9.3

###### vagrant & berkshelf

    gem install vagrant berkshelf

###### the ubuntu 12.04 vagrant box

    vagrant box add precise64 http://files.vagrantup.com/precise64.box

### Howto use?

With the above installed, you should be able to

    hg clone ssh://hg@bitbucket.org/captnswing/graphite_vagrant
    cd graphite_vagrant
    vagrant up
    
This will run the [graphite cookbook](https://github.com/captnswing/chef-graphite) and install graphite and its requirements.

On my machine