# -*- mode: ruby -*-

Vagrant.configure('2') do |config|
  config.vm.hostname = 'sovereign.local'
  config.vm.network 'private_network', ip: '172.16.100.2'

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'site.yml'
    ansible.host_key_checking = false
    ansible.extra_vars = { ansible_ssh_user: 'ubuntu', testing: true }
    ansible.groups = {
      "testing" => ["xenial"]
    }

    # ansible.tags = ['blog']
    # ansible.skip_tags = ['openvpn']
    # ansible.verbose = 'vvvv'
  end

  config.vm.provider :virtualbox do |v|
    v.memory = 512
  end

  config.vm.provider :vmware_fusion do |v|
    v.vmx['memsize'] = '512'
  end

  # vagrant-cachier
  #
  # Install the plugin by running: vagrant plugin install vagrant-cachier
  # More information: https://github.com/fgrehm/vagrant-cachier
  if Vagrant.has_plugin? 'vagrant-cachier'
    config.cache.enable :apt
    config.cache.scope = :box
  end

  # Ubuntu 16.04 (LTS) 64-bit (currently unavailable)
  config.vm.define 'xenial', primary: true do |xenial|
    xenial.vm.box = 'ubuntu/xenial64'
  end
end
