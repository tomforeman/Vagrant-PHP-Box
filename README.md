# Vagrant PHP Box

A Vagrantfile & Puppet manifest that will set you up with:

* Apache
* MySQL
* PHP

## Using as a Git Submodule in your project

First, **make sure any [System Prerequisites](#system-prerequisites) are satisfied** (see below).

    cd ~/Sites/myproject
    git submodule add https://github.com/galbus/Vagrant-PHP-Box.git vagrant
    git commit -m 'commit for submodule vagrant'
    cd vagrant
    vagrant up

Next,

    sudo vi /etc/hosts

and add the following host:

    10.33.33.10 app.local

Assuming that your DocumentRoot is `/public/`, your site will now be available at http://app.local.

If required, the DocumentRoot and other VM/LAMP settings can be adjusted in the config files...

_(Use_ `vagrant reload` _after changing any settings)_

### Vagrantfile

`Vagrantfile`

The Vagrantfile is mainly used to set the VM URL, hostname and VM params (e.g. memory) as well as set the Puppet file paths.

### Puppet Manifest

`puppet/manifests/site.pp`

The Puppet files deal with the installation of Apache, MySQL and PHP and any other other terminal commands that are applied to the VM when it is set up.

### Virtual Hosts

`puppet/manifests/vhosts/app.local.pp`

To add more vhosts simply drop more `*.pp` files into this directory.

## System Prerequisites

Instructions for installing required programs on OSX Mountain Lion.

### XCode & Command Line Tools

* Install XCode from App Store
* Install Command Line Tools using `XCode > Preferences > Downloads`

### RVM

OSX comes it's own copy of Ruby but we really want to leave this alone and use RVM.

1. Install RVM

        curl -L https://get.rvm.io | bash -s stable

2. Verify RVM install

        rvm --version

3. Install Ruby

        rvm install 2.1.0

  **If you get brew errors** then run the following (instructions from [here](http://stackoverflow.com/a/14539521) and [here](http://stackoverflow.com/a/11706900))

      sudo chown -R $USER /usr/local/include
      sudo chgrp -R admin /usr/local
      sudo chmod -R g+rwx /usr/local
      sudo chmod -R o-w /usr/local
      brew update
      brew doctor

  Then

      rvm install 2.1.0

4. Set default Ruby version

        rvm --default use 2.1.0

5. Close and reopen all Terminal windows
   
6. Verify Ruby version

        ruby -v

### VirtualBox

VirtualBox 4.2 is required!

Download this version from https://www.virtualbox.org/wiki/Download_Old_Builds_4_2.

### Vagrant

Download and install the latest version from http://www.vagrantup.com.

### Puppet

The Puppet site recommends installing Puppet, Facter and Hiera from packages, but I found this only caused problems across different OSX platforms.

Instead, install using:

`gem install puppet`

And it all works OK for me.

## DO NOT...

**DO NOT** `gem install vagrant`. Install the Vagrant binary from www.vagrantup.com.

**DO NOT** `gem install librarian-puppet`. The Gem install of Librarian only works with the native Puppet package - we use the Gem package due to install issues across OSX versions.

## TODO

Add support for...

1. CentOS/RHEL (e.g. use yum instead of apt-get)
2. MySQL schema import on provisioning
3. MySQL updates
4. Use YAML config file instead of editing Vagrantfile and site.pp
5. Node.js
6. Mongo/Redis
7. Clusters

## References & Further Reading

* http://pragmaticstudio.com/blog/2010/9/23/install-rails-ruby-mac
* http://joshuaestes.me/post/46145838113/vagrant-puppet-and-symfony2-the-three-musketeers
* https://github.com/patrickdlee/vagrant-examples
* http://stackoverflow.com/questions/16871685/permission-denied-issues-when-use-rvm-install-ruby-2-0-0
* https://sites.google.com/site/timyimblog/blog/deploying-php53-on-centos-with-puppet#TOC-Full-Version-of-php.pp
* http://www.littlehart.net/atthekeyboard/2012/04/15/build-php-54-on-centos-with-vagrant/
* http://blog.servergrove.com/2013/01/11/creating-development-environments-with-vagrant-and-puppet/
* https://ask.puppetlabs.com/question/67/unable-to-run-puppet-on-osx-mountain-lion/
