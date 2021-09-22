# Work Bench Network Services

This Repository is primarily meant as a testdrive for Ansible together with a couple of virtual Juniper machines

## Getting Started

These instructions will prepare the basic setup with an example lab for a small Junos network staged with a Ubuntu server and some basic config by an Ansible host. Copy the project files form Git and make sure the host system meets the prerequisites.

### Prerequisites

* Install vagrant https://www.vagrantup.com/downloads.html
* Install Virtualbox https://www.virtualbox.org/wiki/Downloads
* Install Junos plugins on the host system

```
vagrant plugin install vagrant-junos
vagrant plugin install vagrant-host-shell
```

### Installing

A step by step series of examples that tell you how to get a development env running

Say what the step will be

```
git clone https://github.com/roelsieg/WB_network-services
cd ~working_dir~/ansible-junos-bootsrap/vagrant
vagrant up
```
### System description
Machines:
* ansible - running Ansible etc.
* vt-ubun - virtual test server to deploy networktools
* spine01 - a Junos machine 
* spine02 - a Junos machine


The Ansible host has roughly the following installed:
* A Python3 build with all essentials to run Ansible
* Ansible - provisioning, configuration management tool
* Napalm - Network Automation and Programmability Abstraction Layer with Multivendor support

The Junos hosts used to test are : juniper/ffp-12.1X47-D15.4-packetmode (fetched automagicaly & prepared by Juniper)

### Network design
```
 Workbench Topology
                          +---------+       
                          | spine01 |----+  
                          +---------+    |  
                            |e1 e2|      |   
                            |     |      |   
                            |     |      |   
                            |     |   +---------+
                            |     |   | ansible |
                            |     |   +---------+
                            |     |      |  | 
                            |     |      |  | 
                            |e1 e2|      |  |       
 +---------+              +---------+    |  |
 | vt-ubun |              | spine02 |----+  |
 +---------+              +---------+       |
      |                                     |
      +-------------------------------------+
```
## Running the playbooks

Temp setting on vt_ubun:

```
sudo vi /etc/ssh/sshd_config
PasswordAuthentication yes
```

sudo /etc/init.d/ssh restart

Start off course with the Prerequisites and Installation. 
Then test the setup by running a first playbook:

[pb_phpipam.yml](./provision/playbooks.md)
```
vagrant ssh ansible
sudo ansible-playbook provision/playbook_0.yml
```


## Deployment

No clue yet howto deploy this on a live system!

## Built With


## Authors

* **Roeland SIegers** - *Initial work* 


