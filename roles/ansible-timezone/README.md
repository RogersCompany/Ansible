Role Name
=========

An [Ansible] role to configure timezone settings

Build Status
------------
[![Build Status](https://travis-ci.org/RogersCompany/ansible-timezone.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-timezone)

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-timezone

# set your desired default timezone

# timezone: 'EST5EDT'
# timezone: 'America/New_York'
timezone: 'UTC'

timezone_update_hardware_clock: false
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
    - role: ansible-timezone
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
