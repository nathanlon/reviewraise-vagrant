# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.insert_key = true

  config.vm.box = "centos-6.4-rr"

  config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130427.box"

  config.vm.network "private_network", ip: "33.33.33.22"

  config.vm.synced_folder "../../reviewraise", "/home/vagrant/reviewraise", type: "nfs"

  config.vm.hostname = "rraise.co"

  config.vm.provider :virtualbox do |vb|
    #vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provider "vmware_fusion" do |v|
    #v.gui = true
    v.vmx["memsize"] = "1024"
    v.vmx["numvcpus"] = "2"
  end

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "../puppet-modules/rraise-dev/manifests"
    puppet.manifest_file = "default.pp"
    puppet.module_path = "puppet-configs/modules"
    puppet.options = "--verbose --debug --hiera_config reviewraise/vagrant/puppet-configs/hiera.yaml --environment dev --show_diff"
    #puppet.options = "--verbose --hiera_config reviewraise/vagrant/puppet-configs/hiera.yaml"
  end

end
