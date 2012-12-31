# graphite-vagrant

### Summary, what is this?

* basically, a [Vagrantfile](http://vagrantup.com/v1/docs/vagrantfile.html) to install [graphite](http://graphite.wikidot.org) into a virtual linux box
* the Vagrantfile uses a [chef cookbook](http://docs.opscode.com/essentials_cookbooks.html) for graphite that [I've written](https://github.com/captnswing/chef-graphite)

This should anyone get up and running with a working graphite box in the matter of a few minutes. 

### Prerequisites?

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

###### ubuntu 12.04 vagrant box

    vagrant box add precise64 http://files.vagrantup.com/precise64.box

### How to use?

With the above installed and in place, you should be able to

    hg clone ssh://hg@bitbucket.org/captnswing/graphite_vagrant
    cd graphite_vagrant
    vagrant up
    
This will run the [graphite cookbook](https://github.com/captnswing/chef-graphite) and install graphite and all of its requirements.

On my Macbook Air, that takes around 7 min. YMMV.

Once the chef run completes, you can access graphite's web GUI through [localhost:8085](http://localhost:8085)

![graphite running](https://bitbucket.org/captnswing/graphite_vagrant/raw/default/graphite_running.png)

You can now send data to carbon on port `2003` by many means, e.g. straight from your Terminal:

    # on a Mac
    echo "my.awesome.data 999" `date -j -f date -j -f "%Y/%m/%d %T" "2009/10/15 04:58:06" +"%s"` | nc localhost 2003
    
    # on any other unix
    echo "my.awesome.data 999" `date +%s` | nc localhost 2003

Yeah!