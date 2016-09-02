# magento2-ansible-vagrant

> Ansible provisioned Ubuntu 16.04 vagrant box for [Magento2](https://github.com/magento/magento2) development. 

Definitely not full-featured but useful to bootstrap a dev project.

## Prerequisites

- Vagrant
- VirtualBox

This box uses [Ansible Local Provisioner](https://www.vagrantup.com/docs/provisioning/ansible_local.html).
As a result, Ansible do **not** need to be installed on the host.

## Base box

[geerlingguy/ubuntu1604](https://atlas.hashicorp.com/geerlingguy/boxes/ubuntu1604/)

## Roles

- Dev tools: git, vim, curl, htop
- PHP (7.0 + Composer + Xdebug)
- Nginx
- Redis (for session, full page cache and frontend cache)
- MariaDB 10.0 (dedicated user and database)
- Magento2 (automated project creation, installation and configuration)
