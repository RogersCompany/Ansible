Role Name
=========

Installs and configures OpenNMS http://www.opennms.org/

Requirements
------------

Install all Ansible role requirements.
````
sudo ansible-galaxy install -r requirements.yml -f
````

Vagrant
-------
Spin up Environment under Vagrant to test.
````
vagrant up
````

Usage
-----
````
user: admin
pass: admin
````

###### Non-Vagrant
Login to WebUI (http://iporhostname:8980/opennms)

###### Vagrant
Login to WebUI (http://127.0.0.1:8980/opennms)

Role Variables
--------------

````
---
# defaults file for ansible-opennms
opennms_debian_repo_key: 'https://debian.opennms.org/OPENNMS-GPG-KEY'
opennms_debian_repos:
  - 'deb http://debian.opennms.org stable main'
  - 'deb-src http://debian.opennms.org stable main'
````

Dependencies
------------

#### GitHub
````
ansible-ntp
ansible-postgresql
ansible-postfix
ansible-oracle-java8
ansible-opennms
````
#### Galaxy
````
RogersCompany.ntp
RogersCompany.postgresql
RogersCompany.postfix
RogersCompany.oracle-java8
RogersCompany.opennms
````
Follow instructions in requirements to install dependencies.

Example Playbook
----------------

#### GitHub
````
---
- name: provisions OpenNMS
  hosts: all
  become: true
  vars:
  roles:
    - role: ansible-ntp
    - role: ansible-postgresql
    - role: ansible-postfix
    - role: ansible-oracle-java8
    - role: ansible-opennms
  tasks:
````
#### Galaxy
````
---
- name: provisions OpenNMS
  hosts: all
  become: true
  vars:
  roles:
    - role: RogersCompany.ntp
    - role: RogersCompany.postgresql
    - role: RogersCompany.postfix
    - role: RogersCompany.oracle-java8
    - role: RogersCompany.opennms
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
