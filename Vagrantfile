# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$profile_path = ["config"]

def loadProfile()
$profile_path.each { |file|
  if file and File.file?(file)
	puts "Loading profile %s\n" % [File.realpath(file)]
	return JSON.parse( IO.read( file ), opts = { symbolize_names: true } )
  end
}
end

profile = loadProfile()

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.insert_key = false

  config.vm.box = profile[:box_name]
  config.vm.box_url = profile[:box_url]

  #
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  config.vm.hostname =  "ranger"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 6080, host: 60080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.50.5"


  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  #
  config.vm.synced_folder "data", "/vagrant_data"
  config.vm.synced_folder "/Users/gautam/.m2/", "/home/vagrant/.m2"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Don't boot with headless mode
    #vb.gui = true
  
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", profile[:vm_mem]]
  end

  args = ""

  #config.omnibus.chef_version = :latest
  #config.berkshelf.berksfile_path = 'Berksfile'
  #config.vm.provision :chef_solo do |chef|
  #  chef.roles_path = "chef/roles"
  #  chef.cookbooks_path = ["chef/site-cookbooks", "chef/cookbooks"]
  #  chef.add_role "dev-setup"
  #end

  #config.vm.provision :ansible do |ansible|
  #  ansible.playbook = "provision/bootstrap.yml"
  #  ansible.extra_vars = profile 
  #end

  #config.vm.provision :ansible do |ansible|
  #  ansible.playbook = "provision/install-ranger.yml"
  #  ansible.extra_vars = profile
  #  ansible.verbose = 'v,v,v'
  #end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provision/dev-setup.yml"
    ansible.extra_vars = profile
    ansible.verbose = 'v,v,v'
  end


  #config.vm.provision :shell, :path => "provision/bootstrap.sh", args: args
  #if "true".casecmp(profile[:rpm_install].to_s) == 0
  #  config.vm.provision shell, :path => "provision/install-ranger.sh", args: args
  #  config.vm.provision :shell, :path => "provision/install-plugins.sh", args: args
  #end

  #if "true".casecmp(profile[:build_ranger].to_s) == 0
    #config.vm.provision "shell", inline: "/usr/bin/python /vagrant/provision/dev-setup.py"
	#provision/dev-setup.py", args: args
  #end

  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with CFEngine. CFEngine Community packages are
  # automatically installed. For example, configure the host as a
  # policy server and optionally a policy file to run:
  #
  # config.vm.provision "cfengine" do |cf|
  #   cf.am_policy_hub = true
  #   # cf.run_file = "motd.cf"
  # end
  #
  # You can also configure and bootstrap a client to an existing
  # policy server:
  #
  # config.vm.provision "cfengine" do |cf|
  #   cf.policy_server_address = "10.0.2.15"
  # end


end
