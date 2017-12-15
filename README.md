# Friday demo of Ansible

## Requirements
* ansible
* virtualbox
* vagrant
* vagrant-hostupdater

## How to spin up servers with Vagrant
```
cd <this directory>
ansible-galaxy install -r misc/requirements.yml
vagrant up
ansible-galaxy install -r friday-demo/requirements.yml
```
This will spin up 4 virtual machines and add the user "ernst" to the machines, copy my public key to authorized_keys and add me to the "admins" group.
It will also generate an ansible inventory file in the `.vagrant` directory. A symlink to the inventory file has been created in the root directory.

## How to destroy setup
```
vagrant destroy -f
```

## Demo steps
Preparation
1. vagrant destroy -f
2. ssh-removeknownhost 18 (a bunch of times)
3. vagrant up
4. ansible-playbook friday-demo/site.yml -i inventory --tags "epel,yum"

Demotime
1. Do slideshow
2. ansible-playbook friday-demo/site.yml -i inventory
3. Show some code snippets (maybe)
4. Change code in git repo
5. ansible-playbook friday-demo/site.yml -i inventory --tags "testapp-get"