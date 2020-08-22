# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    servers = [{
        :hostname => "master",
        :ram => 2048,
        :size => "35GB",
        :primary => true,
        :ip => "192.168.2.10",
        :mac => "EE4E228EF848"
    }, {
        :hostname => "node",
        :ram => 2048,
        :size => "15GB",
        :ip => "192.168.2.11",
        :mac => "AAC856C806F1"
    }]

    servers.each do |machine|
        config.vm.define machine[:hostname], primary: machine[:primary], autostart: !machine[:primary].nil? do |node|
            node.vm.box = "ubuntu/bionic64"
            node.vm.network :private_network, ip: machine[:ip]
            node.ssh.forward_agent = true
            node.ssh.forward_x11 = true

            if Vagrant.has_plugin?('vagrant-hosts')
                node.vm.provision :hosts, :sync_hosts => true
            end
            if Vagrant.has_plugin?('vagrant-hostmanager')
                node.vm.hostname = machine[:hostname]
            end
            if Vagrant.has_plugin?('vagrant-disksize')
                node.disksize.size = machine[:size]
            end
            if Vagrant.has_plugin?('vagrant-timezone')
              node.timezone.value = :host
            end

            node.vm.provider :virtualbox do |vb|
              vb.linked_clone = true
              vb.memory = machine[:ram]
              vb.customize ["modifyvm", :id, "--macaddress1", machine[:mac]]
            end

            node.vm.synced_folder "./provisioning", "/home/vagrant/provisioning"
            node.vm.synced_folder "../shared_folder", "/home/vagrant/shared_folder"
        end
    end

    config.vm.provision 'ansible_local' do |ansible|
      ansible.playbook = 'provisioning/playbook.yml'
    end
end
