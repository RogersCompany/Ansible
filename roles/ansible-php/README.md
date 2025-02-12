Role Name
=========

An [Ansible] role to install various PHP packages.

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-php
php_debian_packages:
  # - 'libapache2-mod-php{{ php_version_debian }}'
  - 'php{{ php_version_debian }}'
  - 'php{{ php_version_debian }}-cli'
  - 'php{{ php_version_debian }}-cgi'
  - 'php{{ php_version_debian }}-curl'
  # - 'php{{ php_version_debian }}-dev'
  # - 'php{{ php_version_debian }}-fpm'
  - 'php{{ php_version_debian }}-gd'
  - 'php{{ php_version_debian }}-json'
  - 'php{{ php_version_debian }}-ldap'
  - 'php{{ php_version_debian }}-mysql'
  # - 'php{{ php_version_debian }}-odbc'
  # - 'php{{ php_version_debian }}-sqlite'
  # - 'php{{ php_version_debian }}-xml'
  # - 'php{{ php_version_debian }}-zip'
php_redhat_packages:
  - 'php'
  - 'php-cli'
  - 'php-curl'
  - 'php-devel'
  # - 'php-fpm'
  - 'php-gd'
  - 'php-json'
  - 'php-ldap'
  - 'php-mysql'
  # - 'php-odbc'
  # - 'php-xml'
  # - 'php-zip'
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
    - role: ansible-php
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

[Ansible]: <https://ansible.com>
