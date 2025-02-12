Role Name
=========

An [Ansible] role to install [Redis]

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-redis
# Defines the addresses that Redis should listen on
redis_bind_addresses:
  # - '0.0.0.0'
  - '127.0.0.1'
  # - '{{ ansible_default_ipv4.address }}'
  # - '{{ ansible_all_ipv4_addresses }}'
  # - '{{ ansible_all_ipv6_addresses }}'
  ## Use the method below if you define redis_bind_interfaces instead of
  ## configuring bind addresses using one of the methods above
  # - >
  #   {% for item in redis_bind_interfaces %}
  #   {{ hostvars[inventory_hostname]['ansible_' + item]['ipv4']['address'] }}
  #   {% if not loop.last %}{% endif %}{% endfor %}
# Define interfaces to bind to if ip addresses are not known
redis_bind_interfaces: []
  # - 'enp0s3'
  # - 'enp0s8'
# Defines if Redis should be clustered
# ***NOT WORKING YET
redis_cluster: false
# Defines if Redis is configured
redis_config_redis: true
# Defines if Redis should run as a daemon
redis_daemonize: true
# Defines the number of databases
redis_databases: '16'
# Redis download info for source based installs
redis_dl_info:
  dest_dir: '/usr/local/src'
  file: 'redis-{{ redis_version }}.tar.gz'
  url: 'http://download.redis.io/releases'
# Defines the directory in which Redis is installed to from source
redis_install_dir: '/var/lib/redis'
# Defines if installed from source rather than package manager
redis_install_from_source: true
# Set the max number of connected clients at the same time
redis_max_clients: '10000'
# Define Redis memory limit
# ex. 2147483648, 2048mb, 2gb
# or use the below calculated value
redis_maxmemory: '{{ (ansible_memtotal_mb | int * redis_maxmemory_size_multiplier) | round | int }}mb'
# Defines if maxmemory settings are applied
redis_maxmemory_config: false
# volatile-lru|allkeys-lru|volatile-random|allkeys-random|volatile-ttl|noeviction
redis_maxmemory_policy: 'noeviction'
redis_maxmemory_samples: '5'
# Define multiplier to calculate redis_maxmemory based on installed total memory
redis_maxmemory_size_multiplier: 0.5
# Define Redis listen port
redis_port: '6379'
# Enable replication (true|false)
redis_replication: false
# Define the master replication address
redis_replication_address: "{{ hostvars[inventory_hostname]['ansible_' + redis_replication_interface]['ipv4']['address'] }}"
# Define the Ansible group which the nodes belong to for replication
# This group must exist.
redis_replication_ansible_group: 'redis'
# Define the interface which should be used for replication
# ex. eth1|enp0s3|enp0s8
redis_replication_interface: 'enp0s3'

# How frequently to snapshot the database to disk
# ex. "900 1" => 900 seconds if at least 1 key changed
redis_save_to_disk:
  - seconds: '900'
    changes: '1'
  - seconds: '300'
    changes: '10'
  - seconds: '60'
    changes: '10000'
# System tweaks specific to Redis performance
redis_sysctl_settings:
  - name: 'net.core.somaxconn'
    value: '{{ redis_tcp_backlog }}'
  - name: 'vm.overcommit_memory'
    value: '1'
# Enable logging to the system logger
redis_syslog_logging: false
# In high requests-per-second environments you need an high backlog in order
# to avoid slow clients connections issues
redis_tcp_backlog: '511'
# Redis user info
redis_user_info:
  home: '{{ redis_install_dir }}'
  name: 'redis'
# Defines the Redis version to install when installing from source
redis_version: '3.2.7'
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
    - ansible-redis
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
[Redis]: <https://redis.io>
