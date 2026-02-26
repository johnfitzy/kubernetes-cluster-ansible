# Kubernetes Cluster Ansible
## Purpose
The goal of this project is to demonstrate how to build a Kubernetes cluster on bare metal or VMs and deploy it to multiple different environments. 
### Inventory/Environments
- Vagrant/Virtual Box
- Home lab (coming soon)
- The plan in the future is to deploy it on some cheap cloud VM's
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
#### Local Development (Devcontainer)
Ansible is run from a devcontainer to ensure a consistent, up-to-date version. You will need:
- [Docker](https://docs.docker.com/engine/install/)
- VS Code with the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension

**1. Open the project in the devcontainer**

Open the project in VS Code, then either accept the "Reopen in Container" popup or run via the command palette (`Ctrl+Shift+P`):
```
Dev Containers: Reopen in Container
```
The first run will pull the image and may take a minute. Subsequent opens are instant.

**2. Start the Vagrant VMs**

From a terminal on your **host machine** (not inside VS Code):
```shell
vagrant up
```
This boots the three VMs without running Ansible. You can verify they are up with:
```shell
vagrant status
```

**3. Install Ansible roles and collections**

From the VS Code terminal (inside the devcontainer):
```shell
ansible-galaxy install -r roles/requirements.yml
ansible-galaxy collection install -r collections/requirements.yml
```

**4. Run the playbook**

```shell
ansible-playbook -i inventory/local_vagrant site.yml --become
```

**Re-running the playbook**

Just re-run step 4. No need to restart the VMs.

**Tearing down**

From the host terminal:
```shell
vagrant destroy -f
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