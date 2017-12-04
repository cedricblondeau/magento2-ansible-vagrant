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
- Magento2 (automated project creation if directory is empty, installation and configuration)

## Get started

### 1. Clone this repository

```bash
git clone https://github.com/cedricblondeau/magento2-ansible-vagrant
```

### 2. Configure

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

### 3. Define a syncing strategy (optional)

See [syncing section](#syncing).
You can skip this step if you just want to try Magento2 and don't need to edit files.

### 4. Up!

```bash
vagrant up
```

### 5. It's ready!

Default base URL is: http://192.168.33.10

## Syncing

By default, Magento2 files live in the box.

It's up to you to configure your preferred sync solution. Here are some ideas:

#### NFS (host => guest)

You can find a commented out statement in Vagrantfile.

Example:

```ruby
  config.vm.synced_folder "../magento2", "/home/vagrant/repos/magento2",
    type: 'nfs', mount_options: ['rw', 'async', 'fsc' ,'actimeo=2']
```

#### NFS (guest => host)

See [vagrant-nfs_guest](https://github.com/Learnosity/vagrant-nfs_guest)

#### Don't sync anything

You could also use your text editor/IDE in the VM. You may want to install a GUI or play with X11 forwarding to do so.

#### Rsync

## FAQ / Common issues

#### It looks like the playbook freezes at the task `magento2 : Create project`

It's probably not frozen. Downloading dependencies can take time and it depends on multiple factors such as internet connection speed and syncing strategy.

#### 502 Bad Gateway when accessing the store after initial setup

It may happen if a step failed during the installation and fpm service did not start properly. As a result, nginx cannot communicate with fpm service.
Restarting the VM or php-fpm (`sudo service php7.0-fpm restart`) may help.
