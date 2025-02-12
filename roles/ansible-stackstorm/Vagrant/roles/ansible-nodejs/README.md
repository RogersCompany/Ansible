Role Name
=========

An [Ansible] role to install [NodeJS]

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-nodejs
nodejs_debian_packages:
  - 'build-essential'
  - 'nodejs'
nodejs_debian_repo_info:
  id: '68576280'
  repo_key: 'https://keyserver.ubuntu.com/pks/lookup?op=get&fingerprint=on&search=0x1655A0AB68576280'
  repos:
    - 'deb https://deb.nodesource.com/node_{{ nodejs_version }} {{ ansible_distribution_release|lower }} main'
    - 'deb-src https://deb.nodesource.com/node_{{ nodejs_version }} {{ ansible_distribution_release|lower }} main'

# Defines nodejs version to install..( 6.x|7.x )
# Ubuntu Precise needs to be 6.x
nodejs_version: '7.x'
```

Dependencies
------------

None

Example Playbook
----------------

```
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-nodejs
  tasks:
```

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com

[Ansible]: <https://www.ansible.com>
[NodeJS]: <https://nodejs.org/en/>
