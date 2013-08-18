# -*- mode: ruby -*-
# vi: set ft=ruby :

# We'll mount the Chef::Config[:file_cache_path] so it persists between
# Vagrant VMs
host_cache_path = File.expand_path("../.cache", __FILE__)
guest_cache_path = "/tmp/vagrant-cache"

# ensure the cache path exists
FileUtils.mkdir(host_cache_path) unless File.exist?(host_cache_path)

Vagrant.configure("2") do |config|
  config.vm.box = "dummyAWS"
  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = ENV['AWS_ACCESS_KEY_ID']
    aws.secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']
    aws.keypair_name = ENV['AWS_KEYPAIR_NAME']

    # us-east-1 64bit Ubuntu 12.04.2 LTS (Precise Pangolin)
    aws.region="us-east-1"
    aws.ami = "ami-7747d01e"
    aws.security_groups = ['vagrant']

    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = "/Users/yamir/.ssh/yencarnacion_key.pem"
  end

  config.vm.provision :shell, :path => "bootstrap.sh"

  # config.vm.provision :chef_client do |chef|
  #    chef.validation_client_name = "webninjapr-validator"
  #    chef.client_key_path ="/Users/yamir/Dropbox/Stuff/WebNinjaCorp/Other/Digital-ID/chef-opscode/yencarnacionATwebninjapr_com.pem"
  #    chef.chef_server_url = "https://api.opscode.com/organizations/webninjapr"
  #    chef.validation_key_path = "/Users/yamir/Dropbox/Stuff/WebNinjaCorp/Other/Digital-ID/chef-opscode/webninjapr_com/webninjapr-validator.pem"
  # end

  config.vm.provision :chef_solo do |chef|
    chef.provisioning_path = guest_cache_path
    chef.log_level         = :debug

    chef.json = {
      
    }

    chef.run_list = %w{
      recipe[docker]
    }
  end
 
  config.vm.synced_folder host_cache_path, guest_cache_path
end

