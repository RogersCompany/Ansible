Role Name
=========

Installs and configures Shorewall firewall (http://shorewall.net)

## Build Status

[![Build Status](https://travis-ci.org/RogersCompany/ansible-shorewall.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-shorewall)

Requirements
------------

None

Role Variables
--------------

[defaults/main.yml](defaults/main.yml)

Dependencies
------------

None

Example Playbook
----------------

````
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-shorewall
  tasks:
````
License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com
