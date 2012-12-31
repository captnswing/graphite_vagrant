# graphite-vagrant

### Summary, what is this?

* basically, a [Vagrantfile](http://vagrantup.com/v1/docs/vagrantfile.html) to install [graphite](http://graphite.wikidot.org) into a virtual linux box
* the Vagrantfile uses a [chef cookbook for graphite](https://github.com/captnswing/chef-graphite) that I've written

This simple setup should get anyone up and running with a working graphite box within a few minutes.

### Prerequisites?

###### virtualbox

    # on a Mac
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
    
This will run the [graphite cookbook](https://github.com/captnswing/chef-graphite) and install graphite and all of its requirements. On my Macbook Air, that takes around 7 min. YMMV.

Once the chef run completes, you can access graphite's web GUI through [localhost:8085](http://localhost:8085)

![graphite running](https://bitbucket.org/captnswing/graphite_vagrant/raw/default/graphite_running.png)

You now have a fully functioning graphite system on a virtual vagrant machine. Start sending some data to carbon on port `2003`, e.g. straight from your Terminal:

    # on a Mac - 'date' on a mac isn't the real thing 
    export LC_ALL=C; epochseconds=`date -j -f "%a %b %d %T %Z %Y" "\`date\`" "+%s"`
    
    # on any other unix
    export LC_ALL=C; epochseconds=`date +%s`
    
    # and then...
    echo "my.awesome.data 999" $epochseconds | nc localhost 2003

Since it's only one single data point, it's going to be hard to see in the default graphite view (try to spot a small blue dot in the lower right corner of the graph). With some fiddling, we can make the data point more visible. Using [this URL](http://localhost:8085/render/?width=600&target=lineWidth%28my.awesome.data%2C5%29&yMin=800&yMax=1200&areaMode=first):

    http://localhost:8085/render/?width=600&target=lineWidth%28my.awesome.data%2C5%29&yMin=800&yMax=1200&areaMode=first

we get

![graphite first data](https://bitbucket.org/captnswing/graphite_vagrant/raw/default/graphite_firstdata.png)

Yay!