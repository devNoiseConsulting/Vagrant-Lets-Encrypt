# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.ssh.forward_agent = true

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.10.19"

  #syncs entire project directory to ~/application on target machine
  config.vm.synced_folder "./share", "/home/vagrant/share"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  #provisions the environment
  config.vm.provision "ansible" do |ansible|
#    ansible.verbose = "v"
    ansible.limit = 'all'
    ansible.extra_vars = { user: "vagrant" }
    ansible.inventory_path = "provisioning/hosts"
    ansible.playbook = "provisioning/letsencrypt.yml"
  end
end
