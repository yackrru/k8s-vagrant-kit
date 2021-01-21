# K8s Vagrant Kit
Local development environment for K8s user, which configured by Vagrant.
All boxes are based on `centos/7` and instances by them are set locale to `JP` by default.
#### Prerequirements
- VirtualBox
- Vagrant
## Overview
Directories in this repository are composed of components as follows.
- ansible
  - **ansible server**
    - ansible 2.9
    - playbooks in this repo are placed in `./ansible/ansible`
    - The playbooks are mounted to `/home/vagrant/ansible` on the vagrant instance.
- kubekit
  - **Local development environment for k8s user**
  - The following packages will be installed by `ansible-playbook`
    - Docker v19.03
    - kubectl v1.19
    - Minikube
- pkg
  - Coming soon
## Quick start
Coming soon.
## Usage for box developer
#### Set Up
First, change directory to `ansible` belongs to root path in this repo and execute the following command to build ansible server.
```bash
$ vagrant up
```
You can connect instance after creating ansible instance:
```bash
$ vagrant ssh
```
Then, checkout a new terminal session on your computer and look up a public key, `ansible/data/id_ecdsa.pub`, without ssh to ansible instance.<br>
Copy the key file you would find to `kubekit/data`.<br>
Change directory to `kubekit` and build vagrant:
```bash
$ vagrant up
```
When initialize by up command is done, ssh to kubekit instance from ansible instance.
```bash
[vagrant@ansible ~]$ ssh vagrant@kubekit.localdomain
The authenticity of host 'kubekit.localdomain (192.168.10.10)' can't be established.
...
Are you sure you want to continue connecting (yes/no)? yes

[vagrant@kubekit ~]$
```
#### Do playbook
```bash
[vagrant@ansible ~]$ cd ansible
[vagrant@ansible ansible]$ pwd
/home/vagrant/ansible
[vagrant@ansible ansible]$ ansible-playbook -i inventory playbook.yml
```