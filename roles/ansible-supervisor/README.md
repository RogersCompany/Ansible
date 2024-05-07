Role Name
=========

An [Ansible] role to install/configure [Supervisor]

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-supervisor
supervisor_python_install: false
supervisor_services:
  - name: 'nginx'
    autorestart: true
    autostart: true
    command: '/usr/sbin/nginx -g "daemon off;"'
    state: 'started'
    username: 'www-data'
```

Dependencies
------------


Example Playbook
----------------

```
---
hosts: all
become: true
vars:
roles:
  - role: ansible-supervisor
tasks:
```

License
-------

BSD

Author Information
------------------

Olivier ROGER
- [@RogersCompany]
- [EveryThingShouldBeVirtual]
- RogersCompany [at] gmail.com

[@RogersCompany]: <https://twitter.com/RogersCompany>
[EveryThingShouldBeVirtual]: <http://everythingshouldbevirtual.com>
[Ansible]: <https://www.ansible.com/>
[Supervisor]: <http://supervisord.org/>
