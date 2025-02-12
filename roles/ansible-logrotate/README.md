Role Name
=========

An [Ansible] role to configure [logrotate] definitions

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-logrotate

# Defines if you want your log files compressed
logrotate_compress: false

# packages drop log rotation information into this directory
logrotate_conf_dir: '/etc/logrotate.d/'

logrotate_config: true

logrotate_configs: []
  # - name: 'apache2'
  #   compress: true
  #   copytruncate: false
  #   create:
  #     mode: '640'
  #     owner: 'root'
  #     group: 'adm'
  #   delaycompress: true
  #   logs:
  #     - '/var/log/apache2/*.log'
  #   # If the log file is missing, go on to the next one without
  #   # issuing an error message.
  #   missingok: true
  #   # Do not rotate the log if it is empty
  #   notifempty: true
  #   postrotate:
  #     - 'if /etc/init.d/apache2 status > /dev/null ; then /etc/init.d/apache2 reload > /dev/null; fi;'
  #   prerotate:
  #     - 'if [ -d /etc/logrotate.d/httpd-prerotate ]; then run-parts /etc/logrotate.d/httpd-prerotate; fi;'
  #   rotate: '14'
  #   rotation: 'daily'
  #   sharedscripts: true
  # - name: 'apt'
  #   compress: true
  #   copytruncate: false
  #   delaycompress: false
  #   logs:
  #     - '/var/log/apt/term.log'
  #     - '/var/log/apt/history.log'
  #   # If the log file is missing, go on to the next one without
  #   # issuing an error message.
  #   missingok: true
  #   # Do not rotate the log if it is empty
  #   notifempty: true
  #   rotate: '12'
  #   rotation: 'monthly'
  #   sharedscripts: false
  # - name: 'dpkg'
  #   compress: true
  #   copytruncate: false
  #   create:
  #     mode: '644'
  #     owner: 'root'
  #     group: 'root'
  #   delaycompress: true
  #   logs:
  #     - '/var/log/dpkg.log'
  #     - '/var/log/alternatives.log'
  #   # If the log file is missing, go on to the next one without
  #   # issuing an error message.
  #   missingok: true
  #   # Do not rotate the log if it is empty
  #   notifempty: true
  #   rotate: '12'
  #   rotation: 'monthly'
  #   sharedscripts: false
  # - name: 'redis-server'
  #   compress: true
  #   copytruncate: true
  #   delaycompress: false
  #   logs:
  #     - '/var/log/redis/*.log'
  #   # If the log file is missing, go on to the next one without
  #   # issuing an error message.
  #   missingok: true
  #   # Do not rotate the log if it is empty
  #   notifempty: true
  #   rotate: '12'
  #   rotation: 'weekly'
  #   sharedscripts: false
  # - name: 'yum'
  #   compress: false
  #   copytruncate: false
  #   create:
  #     mode: '0600'
  #     owner: 'root'
  #     group: 'root'
  #   delaycompress: false
  #   logs:
  #     - '/var/log/yum.log'
  #   # If the log file is missing, go on to the next one without
  #   # issuing an error message.
  #   missingok: true
  #   # Do not rotate the log if it is empty
  #   notifempty: true
  #   rotation: 'yearly'
  #   sharedscripts: false
  #   Log files are rotated when they grow bigger then size bytes.  If
  #   size  is  followed by M, the size if assumed to be in megabytes.
  #   If the k is used, the size is in kilobytes. So  size  100,  size
  #   100k, and size 100M are all valid.
  #   size: '30k'

# create new (empty) log files after rotating old ones
logrotate_create_new: true

logrotate_default_backlogs_rotate: '4'

logroate_default_configs:
  - 'apt'
  - 'dpkg'
  - 'rsyslog'
  - 'ufw'

# Defines the default rotate schedule
# hourly | daily | weekly | monthly
logrotate_default_rotate: 'weekly'

# Defines if logrotate configs defined in logroate_default_configs
# should be removed or not
logrotate_remove_default_configs: false
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
    - role: ansible-logrotate
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
[Ansible]: <https://www.ansible.com>
[logrotate]: <http://www.linuxcommand.org/man_pages/logrotate8.html>
