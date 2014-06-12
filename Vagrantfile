# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "trusty"
  config.vm.box_url = 'https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box'


  config.vm.provision :hosts do |provisioner|
    provisioner.add_host '192.168.50.10', ['bacula.internal.local', 'bacula']
  end

  config.vm.define 'bacula' do |node|
    node.vm.hostname = 'bacula.internal.local'
    node.vm.network "private_network", ip: "192.168.50.10"

    node.vm.provision "puppet" do |puppet|
      puppet.manifests_path    = "puppet/manifests/"
      puppet.manifest_file     = "bacula.internal.local.pp"
      puppet.module_path       = "puppet/modules/"
      puppet.options           = "--verbose --debug"
    end
  end
end
