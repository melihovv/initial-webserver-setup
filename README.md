# Initial Server Setup

## inventory file

Create `inventory` file. Its content is something like this

```
[web]
46.101.210.137
```

## Install deps
```bash
ansible-galaxy install -r requirements.yml
```

## Initial setup

By default on ubuntu 16.04 there is no python 2 and aptitude.
To fix it run

```bash
ansible-playbook initial-setup.yml
```
