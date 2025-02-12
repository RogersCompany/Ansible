Role Name
=========

Changes the hostname on a node to match the inventory hostname.

Build Status
------------

[![Build Status](https://travis-ci.org/RogersCompany/ansible-change-hostname.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-change-hostname)

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-change-hostname

# Defines if the node should reboot after changing the hostname
change_hostname_reboot: true
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-change-hostname
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
