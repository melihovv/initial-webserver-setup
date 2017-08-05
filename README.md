# Initial Ubuntu 16.04 Web Server Setup

## What this playbook does

- install python2 and aptitude
- upgrade all software
- create user with sudo rights
- configure sshd: disables root login and password authentication, also allows 
to login only user created on previous step
- install
  - git
  - ntp
  - vim
  - tmux
  - htop
  - curl
- configure automatic security updates (do not reloads server, only installs updates)
- setup timezone
- configure iptables and fail2ban
- create swap file
- setup ssl certificate with letsencrypt
- install node.js, npm and yarn
- install nginx
- install php and composer
- install mysql
- setup zero time deployment for laravel application

## inventory file

Create `inventory` file in project root. You should specify ip address of your
server in this file.

```
[web]
46.101.210.137
```

## Install dependencies

```bash
ansible-galaxy install -r requirements.yml
```

## Initial setup

By default on ubuntu 16.04 there is no python 2 and aptitude. Without those
programs ansible cannot work. To fix it run:

```bash
ansible-playbook initial-setup.yml
```

Beside it this playbook also creates user and configures ssh server.

## Environment variables

Copy `vars/main.yml.example` to `vars/main.yml` and change variable values for
your needs. For security reasons you may want to encrypt this file using
ansible-vault:
```bash
ansible-vault encrypt vars/main.yml
```
And then edit this file
with
```bash
ansible-vault edit vars/main.yml
```

To see all available variables take a look at `roles/*/defaults/main.yml`. Also
visit external roles github page for additional documentation.

### To generate password use

```bash
sudo apt-get install -y whois
mkpasswd --method=SHA-512
```

## Provision server

This playbook setup nginx, php-fpm, mysql, nodejs, etc.

```bash
ansible-playbook setup.yml
```

### To run only specific roles

```bash
ansible-playbook setup.yml --tags=user,nginx
```

### To exclude specific roles

```bash
ansible-playbook setup.yml --skip-tags=user,nginx
```

## Deploy

```bash
ansible-playbook deploy.yml
```

## Security

If you discover any security related issues, please email amelihovv@ya.ru instead of using the issue tracker.

## Credits

- [Alexander Melihov](https://github.com/melihovv)
- [All contributors](https://github.com/melihovv/initial-webserver-setup/graphs/contributors)
