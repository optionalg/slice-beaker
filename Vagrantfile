# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'vagrant-openstack-provider'
require 'securerandom'

Vagrant.configure('2') do |config|

  config.vm.box               = 'dummy'
  config.ssh.username         = ENV['PLATFORM'].split('-')[0]
  config.ssh.pty              = true
  config.ssh.private_key_path = "#{ENV['HOME']}/.ssh/vagrant.pem"

  config.vm.provider :openstack do |os|
    os.server_name        = "slice-beaker-#{ENV['MODULE']}-#{SecureRandom.hex(4)}"
    os.openstack_auth_url = ENV['OS_AUTH_URL']
    os.username           = ENV['OS_USERNAME']
    os.password           = ENV['OS_PASSWORD']
    os.tenant_name        = ENV['OS_PROJECT_NAME']
    os.flavor             = 'g1.medium'
    os.image              = ENV['PLATFORM'].gsub('-', '_')
    os.floating_ip_pool   = 'ext-net-pdx1-opdx1'
    os.keypair_name       = 'vagrant'
    os.security_groups    = ['sg0']
  end

  config.vm.provision "shell", path: "beaker.sh", args: [ ENV['MODULE'], ENV['PLATFORM'] ], privileged: false
end
