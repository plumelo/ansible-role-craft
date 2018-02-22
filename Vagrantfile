# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.hostname = 'craft'
  config.vm.box = 'plumelo/xenial64'

  config.ssh.forward_agent = true

  config.vm.provider :lxc do |lxc|
    lxc.container_name = 'craft'
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'test/test.yml'
    ansible.galaxy_role_file = 'test/galaxy.yml'
  end
end
