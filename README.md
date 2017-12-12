# Friday demo of Ansible

## Requirements
* ansible
* virtualbox
* vagrant

## How to spin up servers with Vagrant
```
cd <this directory>
ansible-galaxy install -r misc/requirements.yml
vagrant up
```
This will spin up 4 virtual machines and add the user "ernst" to the machines, copy my public key to authorized_keys and add me to the "admins" group.
It will also generate an ansible inventory file in the `.vagrant` directory. A symlink to the inventory file has been created in the root directory.