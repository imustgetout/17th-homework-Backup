# -*- mode: ruby -*-
# vi: set ft=ruby :

MACHINES = {
:backupServer => {
        :box_name => "centos/7",
	:ip_addr => '192.168.50.11'
  },
  :backupClient => {
        :box_name => "centos/7",
	:ip_addr => '192.168.50.12'
  },
}

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end

  config.vm.define "backupClient" do |client|
    client.vm.network "private_network", ip: "192.168.50.11", virtualbox__intnet: "net1"
    client.vm.host_name = "backupClient"
    client.vm.provision "ansible" do |ansible|
      ansible.playbook = "client.yml"
     end	
  end

  config.vm.define "backupServer" do |server|
    server.vm.network "private_network", ip: "192.168.50.10", virtualbox__intnet: "net1"
    server.vm.hostname = "backupServer"
    server.vm.provision "ansible" do |ansible|
      ansible.playbook = "server.yml"
     end	
  end

end
