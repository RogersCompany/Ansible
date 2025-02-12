Role Name
=========

An [Ansible] role to install [MongoDB]

Requirements
------------

If setting up replication, ensure that DNS works between hosts or
update /etc/hosts appropriately.

Role Variables
--------------

```
---
# defaults file for ansible-mongodb
mongodb_admin_user:
    name: 'admin'
    password: 'admin'
    database: 'admin'
    roles:
      - 'userAdminAnyDatabase'
    state: 'present'

mongodb_apt_keyserver: 'keyserver.ubuntu.com'
mongodb_apt_gpg_key: 'EA312927'

# Defines the binding IP address for MongoDB to listen on
# Ensure to change from default (127.0.0.1) if setting up replication
mongodb_bind_ip:
  # - '0.0.0.0'
  - '127.0.0.1'
  # - '{{ ansible_enp0s8.ipv4.address }}'

# Defines the path to the MongoDB configuration file
mongodb_config: '/etc/mongod.conf'

# Defines if MongoDB should be configured
mongodb_config_mongodb: false

# Defines if MongoDB users should be created.
mongodb_create_users: false

# Defines the path to store MongoDB
mongodb_dbPath: '/var/lib/mongodb'
mongodb_debian_apt_repo: 'deb http://repo.mongodb.org/apt/{{ ansible_distribution|lower }} {{ ansible_distribution_release }}/mongodb-org/{{ mongodb_version }} main'

# Defines the listen port for MongoDB
mongodb_port: '27017'

mongodb_redhat_repo_info:
  name: 'MongoDB-Repository'
  description: 'MongoDB-Repository'
  baseurl: 'https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/{{ mongodb_version }}/x86_64/'
  gpgcheck: yes
  enabled: yes
  gpgkey: 'https://www.mongodb.org/static/pgp/server-{{ mongodb_version }}.asc'

# Defines if MongoDB replication is configured
mongodb_replication: false

# Defines the Ansible group which contains the hosts to setup replication
mongodb_replication_group: 'test-nodes'

# Defines the keyFile to setup replication if using authentication
mongodb_replication_keyfile: '{{ mongodb_dbPath }}/keyFile'

# Defines the node which should be considered the replication master
mongodb_replication_master: '{{ groups[mongodb_replication_group][0] }}'

# Defines the replication set name when setting up replication
mongodb_replication_set: 'rs0'

# Defines the system log for MongoDB
mongodb_systemlog_path: '/var/log/mongodb/mongod.log'

mongodb_ubuntu_apt_repo: 'deb http://repo.mongodb.org/apt/{{ ansible_distribution|lower }} {{ ansible_distribution_release }}/mongodb-org/{{ mongodb_version }} multiverse'

# Defines the users to create if mongodb_create_users is true
mongodb_users:
  - name: 'testuser'
    password: 'testuser'
    database: 'test'
    roles:
      - 'readWrite'
      # - 'readWriteAnyDatabase'
    state: 'present'

# Define MongoDB version to install
mongodb_version: '3.2'
```

Dependencies
------------

None

Example Playbook
----------------
```
---
- hosts: test-nodes
  become: true
  vars:
    pri_domain_name: 'test.vagrant.local'
  roles:
    - role: ansible-mongodb
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
[MongoDB]: <https://www.mongodb.org/>
