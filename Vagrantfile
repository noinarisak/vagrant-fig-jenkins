# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?("vagrant-vbguest")
  raise 'vagrant-vbguest is not installed!'
end

unless Vagrant.has_plugin?("vagrant-cachier")
  raise 'vagrant-cachier is not installed!'
end

unless Vagrant.has_plugin?("vagrant-hostmanager")
  raise 'vagrant-hostmanager is not installed!'
end

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "99designs/ubuntu-docker"
  
  if Vagrant.has_plugin?('vagrant-cachier')
    config.cache.scope = :box
  end

  if Vagrant.has_plugin?('vagrant-hostmanager')
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
    config.vm.define 'vagrant-ubuntu-docker' do |node|
      node.vm.hostname = 'docker-dev-box'
      node.vm.network :private_network, ip: '192.168.42.42'
      node.hostmanager.aliases = %w(vagrant-ubuntu-docker.localdomain jenkins.dev)
    end
  end

  # config.vm.box_check_update = false
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  # config.ssh.forward_agent = true
  config.vm.synced_folder ".", "/vagrant"
  
  config.vm.provision :shell, :inline => <<-SCRIPT
    #apt-get update
    DEBIAN_FRONTEND=noninteractive apt-get -y -q install vim git subversion python-pip
    sudo pip install -U fig
  SCRIPT

  # config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end

end
