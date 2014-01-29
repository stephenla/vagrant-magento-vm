# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # Lucky people can enable nfs but they will get permission errors https://groups.google.com/forum/?fromgroups=#!topic/vagrant-up/-J3UEqYXveA
config.vm.synced_folder ".", "/vagrant", :mount_options => ['dmode=777','fmode=777']

  config.vm.provider :virtualbox do |vb|
  
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end
  
  config.vm.provision :chef_solo do |chef|
    # Specify vagrant cookbooks: our project cookbooks and magento required cookbooks
    chef.cookbooks_path = ["./myrecipes/cookbooks", "./recipes/cookbooks",]
    #chef.roles_path = "./recipes/roles"
    #chef.data_bags_path = "./recipes/data_bags"
    chef.add_recipe "vagrant_magento"

    # You may also specify custom JSON attributes:
    chef.json = { 
        'vagrant_magento' => {
            'config' => {
                'install' => true,
            },
            'source' => {
                'version' => 'magento-1.8.0.0-alpha1',
            },
            'sample_data' => {
                'install' => true,
                'version' => '1.6.1.0',
            },
            # Sets MAGE_IS_DEVELOPER_MODE (error reporting)
            'mage_dev_enabled' => true,

            # Install Magneto Debug
            'debug' => {
                'enabled' => true,
            }
        },
    }
    #chef.log_level = :debug

  end

end
