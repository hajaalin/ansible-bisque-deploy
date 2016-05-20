# -*- mode: ruby -*-
# vi: set ft=ruby :
require_relative './vagrant/key_authorization'

Vagrant.configure('2') do |config|
#  config.vm.box = 'ubuntu/trusty64'
  config.vm.box = 'ubuntu/trusty64'
  #config.vm.box = 'ubuntu/precise64'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :virtualbox do |v|
       v.memory = 2048
       v.cpus = 2
  end

  # {
  #   'bisque'   => '192.168.40.11',
  #   #'bisque2'   => '192.168.40.12',
  #   #'db'   => '192.168.40.21',
  # }.each do |short_name, ip|
  [
    ['bisque', '192.168.40.11', 'ubuntu/trusty64'],
    ['bisque3', '192.168.40.13', 'debian/jessie64']
    #'db'   => '192.168.40.21',
  ].each do |vm_spec|
    short_name = vm_spec[0]
    ip = vm_spec[1]
    box = vm_spec[2]
    config.vm.define short_name do |host|
      host.vm.box = box
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}.lmu.dev"
      host.vm.synced_folder ".", "/home/vagrant/sync", disabled: true
    end
  end
end
