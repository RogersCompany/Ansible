Role Name
=========

Installs Kodi (https://kodi.tv/)

Requirements
------------

None

Role Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------

````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-kodi
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
