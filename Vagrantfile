# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    # Configure cached packages to be shared between instances of the same base box.
    # More info on http://fgrehm.viewdocs.io/vagrant-cachier/usage
    config.cache.scope = :box

    config.cache.synced_folder_opts = {
      type: :nfs,
      mount_options: ['rw', 'vers=3', 'tcp', 'nolock']
    }
    # For more information see https://docs.vagrantup.com/v2/synced-folders/nfs.html
  end

  # Centos
  config.vm.define :centos65, :autostart => false do |vmconfig|
    vmconfig.vm.box = "puppetlabs/centos-6.5-64-puppet"
    vmconfig.vm.network :private_network, ip: "192.168.72.10"
    config.vm.provision "shell", inline: "sudo yum install -y vim"
  end

  config.vm.define :centos7, :autostart => false do |vmconfig|
    vmconfig.vm.box = "puppetlabs/centos-7.0-64-puppet"
    vmconfig.vm.network :private_network, ip: "192.168.72.10"
    config.vm.provision "shell", inline: "sudo yum install -y vim"
  end

  # Ubuntu
  config.vm.define :precise, :autostart => false do |vmconfig|
    vmconfig.vm.box = "puppetlabs/ubuntu-12.04-64-puppet"
    vmconfig.vm.network :private_network, ip: "192.168.72.10"
    config.vm.provision "shell", inline: "sudo apt-get install -y vim"
  end

  config.vm.define :trusty, :autostart => false do |vmconfig|
    vmconfig.vm.box = "puppetlabs/ubuntu-14.04-64-puppet"
    vmconfig.vm.network :private_network, ip: "192.168.72.10"
    config.vm.provision "shell", inline: "sudo apt-get install -y puppet vim"
  end

  # Puppet is commented out by default because maybe you want to SSH to the host and do a noop
  #
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "puppet/manifests"
  #   puppet.manifest_file  = "site.pp"
  #   puppet.module_path    = "puppet/modules"
  #   puppet.options        = "--verbose --show_diff"
  # end
  config.vm.provision "shell", inline: "echo 'sudo puppet apply /vagrant/puppet/manifests/site.pp --modulepath /vagrant/puppet/modules' > /runpuppet.sh && chmod a+x /runpuppet.sh"
  config.vm.provision "shell", inline: "echo 'sudo puppet apply /vagrant/puppet/manifests/site.pp --modulepath /vagrant/puppet/modules --noop' > /runpuppetnoop.sh && chmod a+x /runpuppetnoop.sh"
end
