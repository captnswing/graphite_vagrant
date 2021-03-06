# graphite-vagrant

### Summary, what is this?

* basically, a [Vagrantfile](http://vagrantup.com/v1/docs/vagrantfile.html) that installs [graphite](http://graphite.wikidot.org) on a virtual linux box
* the Vagrantfile uses a [chef cookbook for graphite](https://github.com/captnswing/chef-graphite) that I've written

This simple setup should get anyone up and running with a working graphite box within a few minutes.

### Prerequisites?

You need [Virtualbox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/). On a Mac, use these steps to install: [https://gist.github.com/captnswing/8158880](https://gist.github.com/captnswing/8158880)

### How to use?

With the above installed and in place, you should be able to simply:

    hg clone ssh://hg@bitbucket.org/captnswing/graphite_vagrant
    cd graphite_vagrant
    vagrant up

This will run the chef-solo provisioner with the [graphite cookbook](https://github.com/captnswing/chef-graphite) and install graphite and all of its requirements on the local vagrant box. On my 2013 Macbook Air, that takes around 4-5 min. YMMV.

### And now what?

Once the chef run completes, you can access graphite's web GUI through [localhost:8085](http://localhost:8085)

![graphite running](https://raw.github.com/captnswing/graphite_vagrant/master/graphite_running.png)

You now have a fully functioning graphite system on a virtual vagrant machine. Start sending some data to carbon on port `2003`, e.g. straight from your Terminal:

    # on a Mac < OS X 10.9 - 'date' isn't quite so good
    export LC_ALL=C; epochseconds=`date -j -f "%a %b %d %T %Z %Y" "\`date\`" "+%s"`

    # on Mac >= 10.9 and any other unix
    epochseconds=`date +%s`

    # and then...
    echo "my.awesome.data 999" $epochseconds | nc localhost 2003

Since that is only one single data point, it's going to be hard to see in the default graphite view (try to spot a small blue dot in the lower right corner of the graph).

With some fiddling in the Graphite GUI, we can make that single data point more visible. Using [this URL](http://localhost:8085/render/?width=600&target=lineWidth%28my.awesome.data%2C5%29&yMin=800&yMax=1200&areaMode=first):

    http://localhost:8085/render/?width=600&target=lineWidth%28my.awesome.data%2C5%29&yMin=800&yMax=1200&areaMode=first

we get:

![graphite first data](https://raw.github.com/captnswing/graphite_vagrant/master/graphite_firstdata.png)

Yay! Make sure to check out the [graphite docs](http://graphite.readthedocs.org/) for more.

Happy graphing!
