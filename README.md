# Light Hosting Gameserver

An opinionated baseline gameserver setup using Ansible.

## Requirements

- Ansible
- At least one server

## Setup

### Ansible

Copy `/ansible/group_vars/all/vars.yml.example` as `/ansible/group_vars/all/vars.yml` to configure ansible.  
Copy `/ansible/inventory.example` as `/ansible/inventory` to configure host inventory, both IPs and DNS entries may be used.

The `root_password` and `user_password` should be the password part of a .htaccess user. After the configuration the user `deploy` should be used.

## Quick start

Create configuration files:

```bash
cp ansible/group_vars/all/vars.yml.example ansible/group_vars/all/vars.yml
cp ansible/inventory.yml.example ansible/inventory.yml
```

Fill in configurations in the two files.

### First run against a new server

The first time running the playbook against a new server, a password for the provider-provisioned root user is required.

```bash
cd ansible
ANSIBLE_CONFIG=ansible.cfg ansible-playbook -i inventory.yml -e ansible_user=root --ask-pass --limit=gameserver.example.com provision.yml
```

This is only required on the first run, as the password will be changed afterwards to match the one defined in the `vars.yml` file, and SSH keys will be set up.

### Subsequent runs

After the first run, the playbook may be invoked normally, as the proper users are in place.

```bash
cd ansible
ANSIBLE_CONFIG=ansible.cfg ansible-playbook -i inventory.yml provision.yml
```

## Inspirations

Light Hosting Gameserver is the first iteration of my personal gameserver setup.

The setup is based on my Kubernetes hosting setup [light-hosting-kube](https://github.com/SorenA/light-hosting-kube) and Resilio setup [light-hosting-resilio](https://github.com/SorenA/light-hosting-resilio).
