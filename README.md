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

## Get started

### Clone this repository

```bash
git clone https://github.com/cedricblondeau/magento2-ansible-vagrant
```

### Configure

Create a dev.yml conf file in ansible/group_vars:

```bash
cd magento2-ansible-vagrant
cp ansible/group_vars/dev.yml.sample ansible/group_vars/dev.yml
```

And configure your environment:

```yaml
magento_account_public_key: YOUR_PUBLIC_KEY_HERE
magento_account_private_key: YOUR_PRIVATE_KEY_HERE
mysql_user: magento2
mysql_password: magento2
mysql_dbname: magento2
magento2_language: en_US
magento2_currency: USD
magento2_admin_user: admin
magento2_admin_password: admin2015
magento2_admin_email: null@magento.com
magento2_admin_firstname: John
magento2_admin_lastname: Doe
magento2_crypt_key: YOUR_CRYPT_KEY
magento2_base_url: http://192.168.33.10
```

### Up!

```bash
vagrant up
```
