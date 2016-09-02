# magento2-ansible-vagrant

> Ansible provisioned Ubuntu 16.04 vagrant box for [Magento2](https://github.com/magento/magento2) development. 

Definitely not full-featured but useful to bootstrap a project.

## Base box

[geerlingguy/ubuntu1604](https://atlas.hashicorp.com/geerlingguy/boxes/ubuntu1604/)

## Roles

- Dev tools: git, vim, curl
- PHP (7.0 + Composer + Xdebug)
- Nginx
- Redis (for session, full page cache and frontend cache)
- MariaDB 10.0 (dedicated user and database)
- Magento2 (automated project creation, installation and configuration)
