#
# Juniper lab v0.1
#
# ge-0/0/0.0: management interface
# ge-0/0/1.0 - ge-0/0/7.0: user interfaces

#default_box = 'image_to_use'
default_box = "juniper/ffp-12.1X47-D15.4-packetmode"

#  Workbench Topology
#                           +---------+       
#                           | spine01 |----+  
#                           +---------+    |  
#                             |e1 e2|      |   
#                             |     |      |   
#                             |     |      |   
#                             |     |   +---------+
#                             |     |   | ansible |
#                             |     |   +---------+
#                             |     |      |  | 
#                             |     |      |  | 
#                             |e1 e2|      |  |       
#  +---------+              +---------+    |  |
#  | vt-ubun |              | spine02 |----+  |
#  +---------+              +---------+       |
#       |                                     |
#       +-------------------------------------+

Vagrant.configure(2) do |config|
  config.vm.box = default_box
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
    vb.gui = false
  end
  config.vm.define 'ansible' do |ansible|
	  ansible.vm.box = "ubuntu/focal64"
	  ansible.vm.network :forwarded_port, guest: 22, host: 12202, id: 'ssh'
	  ansible.vm.network "private_network", virtualbox__intnet: "ans_s01",
                    ip: "10.0.1.1",
                    netmask: "255.255.255.252",
									  auto_config: true
	  ansible.vm.network "private_network", virtualbox__intnet: "ans_s02",
                    ip: "10.0.1.5",
                    netmask: "255.255.255.252",
									  auto_config: true
	  ansible.vm.network "private_network", virtualbox__intnet: "ans_ipam",
                    ip: "10.0.1.9",
                    netmask: "255.255.255.252",
									  auto_config: true	
	  ansible.vm.provision "file", source: "ansible.cfg", destination: "ansible.cfg" 
    ansible.vm.provision "file", source: "provision", destination: "provision"
	  ansible.vm.provision 'shell', inline: <<-SHELL
      sleep 30
	    sudo /vagrant/install.sh
      SHELL
  end

  config.vm.define 'vt_ubun' do |vt_ubun|
	  # vt_ubun.vm.box = "ubuntu/bionic64"
    # vt_ubun.vm.box = "ubuntu/focal64"
    vt_ubun.vm.box = "ubuntu/xenial64"
	  vt_ubun.vm.provider "virtualbox" do |vb|
		  vb.memory = 8192
		  vb.cpus = 2
		  vb.gui = false
	  end
	  vt_ubun.vm.network :forwarded_port, guest: 80, host: 8080, id: 'http'
	  vt_ubun.vm.network :forwarded_port, guest: 22, host: 12203, id: 'ssh'
	  vt_ubun.vm.network "private_network", virtualbox__intnet: "ans_ipam",
                    ip: "10.0.1.10",
                    netmask: "255.255.255.252",
									  auto_config: true
    end

  config.vm.define 'spine01' do |spine01|
	  spine01.vm.host_name = "spine01"
	  spine01.vm.network :forwarded_port, guest: 22, host: 2204, id: 'ssh'
    spine01.vm.network 'private_network',
                    virtualbox__intnet: 's01_s02',
                    ip: '169.254.12.11', auto_config: false, nic_type: "virtio"
	  spine01.vm.network "private_network", 
					          virtualbox__intnet: "ans_s01",
                    ip: "10.0.1.2",
                    netmask: "255.255.255.252",
					          nic_type: "virtio"
  end
  
  config.vm.define 'spine02' do |spine02|
    spine02.vm.host_name = "spine02"
	  spine02.vm.network :forwarded_port, guest: 22, host: 2205, id: 'ssh'
    spine02.vm.network 'private_network',
                    virtualbox__intnet: 's01_s02',
                    ip: '169.254.21.11', auto_config: false, nic_type: "virtio"
	  spine02.vm.network "private_network", 
					          virtualbox__intnet: "ans_s02",
                    ip: "10.0.1.6",
                    netmask: "255.255.255.252",
					          nic_type: "virtio" 
  end
end


