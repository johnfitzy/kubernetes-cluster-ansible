# Kubernetes Cluster Ansible
## Purpose
The goal of this project is to demonstrate how to build a Kubernetes cluster on bare metal or VMs and deploy it to multiple different environments. 
### Inventory/Environments
- Vagrant/Virtual Box
- Home lab (coming soon)
- The plan in the future is to deploy it on some cheap cloud VM's
## Dependencies
### Ansible
Ansible version is core 2.19.0. To install do:
```shell
sudo apt install python3-venv -y
python3 -m venv ~/venvs/ansible
source ~/venvs/ansible/bin/activate
pip install ansible-core==2.19.0
```
Then `source path/to/venv/bin/activate`
### Vagrant
- Install Vagrant and Virtual Box-
## Inventories
### Vagrant
- Add the following to your hosts file:
```shell
192.168.56.111 srv1
192.168.56.112 srv2
192.168.56.113 srv3
```
#### Deploy to Vagrant
Then from the root of the project:
```shell
vagrant up
```
You should then be able to ssh to each node with `vagrant ssh ${node_name}`
#### Re-running plays
Run:
```shell
vagrant provision
```
### Home Servers
- This is a for sure a work in progress.... Currently, I only have three Lenovo m910q machines plugged straight into my ISP modem (It's not serving anything to the internet). 
- I plan to extend this with a pfsense or opnsense firewall and implement vLANs, VPN and isolate everything from my home devices before serving anything over the internet.

|  Host   |      Host 1       |     Host 2     |       Host 3        |
|:-------:|:-----------------:|:--------------:|:-------------------:|
|  Model  |   Lenovo m910q    |  Lenovo m910q  |    Lenovo m910q     |
|   CPU   |  Intel i5 7500T   | Intel i5 7500T |   Intel i5 7500T    |
|   RAM   |        8GB        |      8GB       |         8GB         |
| Storage |     256GB NVM     |      256GB NVM       |         256GB NVM        |
|   NIC   | Intel 1Gb I219-LM |      Intel 1Gb I219-LM       |         Intel 1Gb I219-LM        |