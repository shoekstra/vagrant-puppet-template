## vagrant-puppet-template
=======

This is a basic Vagrantfile template with different OSes preconfigured to quickly get the ball rolling.  None of the boxes will autostart with a `vagrant up`, so you need to specify the box name as a parameter.  You can see available boxes by doing `vagrant box list`.

### Installing Vagrant plugins

There is no plugin manager for Vagrant, but as they're just gems we can put them in a Gemfile and use bundler to install them.

```
bundle install
```

### Preinstalling Vagrant boxes

You can preinstall Vagrant boxes that already have Puppet installed by doing the following.

```
for box in `grep puppetlabs Vagrantfile | awk '{print $3}' | sed s/\"//g`; do vagrant box add $box --provider virtualboxl; done
```

Alternatively, if you don't have the required box it will be downloaded the first time you do a `vagrant up`

### Adding more Vagrant boxes

Adding more Vagrant boxes is as [grabbing one of the prebaked Puppet boxes](https://vagrantcloud.com/puppetlabs) and referencing the box name in your new vm configuration.

