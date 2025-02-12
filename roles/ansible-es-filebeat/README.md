Role Name
=========

An [Ansible] role to install/configure [Elastic Filebeat]

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-es-filebeat
es_filebeat_debian_package: 'filebeat-{{ es_filebeat_version }}-amd64.deb'
es_filebeat_dl_url: 'https://artifacts.elastic.co/downloads/beats/filebeat'

# Define filebeat config per
# https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-configuration-details.html
# The config here will be automatically converted to proper YAML for Filebeat
# /etc/filebeat/filebeat.yml using the Jinja2 template.
es_filebeat_config:
  filebeat.prospectors:
    - paths:
      - '/var/lib/docker/containers/*/*.log'
      encoding: 'plain'
      input_type: 'log'
      json.add_error_key: true
      json.keys_under_root: true
      json.message_key: 'log'
      document_type: 'docker-logs'
  logging:
    level: 'debug'
    to_files: true
    to_syslog: false
    files:
      path: '/var/log'
      name: 'filebeat.log'
      keepfiles: 7
  output:
    elasticsearch:
      hosts:
      - 'http://192.168.250.14:9200'
      - 'http://192.168.250.15:9200'
      index: 'filebeat'
      template:
        name: 'filebeat'
        path: '/etc/filebeat/filebeat.template.json'
  registry_file: '/var/lib/filebeat/registry'

es_filebeat_redhat_package: 'filebeat-{{ es_filebeat_version }}-x86_64.rpm'

# Event count spool threshold - forces network flush if exceeded
es_filebeat_spool_size: 2048
es_filebeat_version: '5.3.2'
```

Dependencies
------------

None

Example Playbook
----------------

```
---
- hosts: docker_hosts
  vars:
    es_filebeat_config:
      filebeat.prospectors:
        - paths:
          - '/var/lib/docker/containers/*/*.log'
          encoding: 'plain'
          input_type: 'log'
          json.add_error_key: true
          json.keys_under_root: true
          json.message_key: 'log'
          document_type: 'docker-logs'
      logging:
        level: 'debug'
        to_files: true
        to_syslog: false
        files:
          path: '/var/log'
          name: 'filebeat.log'
          keepfiles: 7
      output:
        elasticsearch:
          hosts:
          - 'http://192.168.250.14:9200'
          - 'http://192.168.250.15:9200'
          index: 'filebeat'
          template:
            name: 'filebeat'
            path: '/etc/filebeat/filebeat.template.json'
      registry_file: '/var/lib/filebeat/registry'
  roles:
    - role: ansible-es-filebeat
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
[Elastic Filebeat]: <https://www.elastic.co/products/beats/filebeat>
