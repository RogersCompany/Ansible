Role Name
=========

An [Ansible] role to install/configure [Sensu] monitoring

Requirements
------------

Install all requirements using Ansible Galaxy.  
```
sudo ansible-galaxy install -r requirements.yml -f
```

Vagrant
-------

Spin up environment using Vagrant.  
```
vagrant up
```

Role Variables
--------------

```
---
# defaults file for ansible-sensu

# Enable user/pass auth for api access
# default is false
# no user/pass required
sensu_api_info:
  auth: false
  host: '{{ sensu_host }}'
  pass: 'sensu'
  port: '4567'
  user: 'sensu'

# sensu_check_plugins:
#   - check-cpu.rb
#   - check-disk.rb
#   - check-es-cluster-status.rb
#   - check-es-file-descriptors.rb
#   - check-es-heap.rb
#   - check-haproxy.rb
#   - check-procs.rb
#   - check-redis-ping.rb
#   - es-cluster-metrics.rb
sensu_checks:
  - name: 'cpu'
    command: 'check-cpu.rb'
    interval: 60
    subscribers:
      - 'test'
      - 'ALL'
    state: 'present'
  - name: 'disk-usage'
    command: 'check-disk-usage.rb -w 80 -c 90'
    interval: 60
    subscribers:
      - 'test'
      - 'ALL'
    state: 'present'
  - name: 'memory'
    command: 'check-memory.rb -w 2500 -c 3000'
    interval: 60
    subscribers:
      - 'test'
      - 'ALL'
    state: 'present'
  - name: 'memory-percent'
    command: 'check-memory-percent.rb -w 70 -c 80'
    interval: 60
    subscribers:
      - 'test'
      - 'ALL'
    state: 'present'
  - name: 'test'
    command: 'echo -n OK'
    interval: 60
    subscribers:
      - 'test'
      - 'ALL'
    state: 'present'

# Defines if host is a sensu client/server
sensu_client: true

sensu_client_debian_packages:
  - erlang-nox
  - build-essential
  - make
  - sensu
  - ruby2.3
  - ruby2.3-dev
sensu_client_address: "{{ ansible_host }}"
sensu_client_services:
  - sensu-client
sensu_client_subscriptions:
  - 'ALL'
  - 'test'
sensu_config_dir: '{{ sensu_root_dir }}/conf.d'

# sensu definitions - added to /etc/sensu/conf.d
sensu_config_handlers_def:
  - handler_default
  - handler_email
  - handler_logstash
  - handler_mailer
  - logstash
  - mailer

# sensu ruby handlers
# added to /etc/sensu/handlers
sensu_config_handlers_mod:
  - logstash
  - mailer

sensu_debian_repo: 'deb https://sensu.global.ssl.fastly.net/apt sensu main'
sensu_debian_repo_key: 'https://sensu.global.ssl.fastly.net/apt/pubkey.gpg'

# leave set to default
# this is a built-in plugin that does nothing
sensu_default_handler: default
sensu_default_handlers:
  - logstash
#  - mailer
sensu_notification_email_from: 'sensu@{{ sensu_smtp_domain_name }}'

# set to email address to send alerts to
sensu_notification_email_to: '{{ sensu_email_notifications }}'
sensu_email_notifications: 'notifications@{{ sensu_pri_domain_name }}'
sensu_enable_cpu_monitors: true
sensu_enable_disk_monitors: true
sensu_enable_es_monitors: false

# to use handlers for events
# configure sensu_config_handlers_def, sensu_config_handlers_mod,
# sensu_default_handler and sensu_default_handlers as appropriate
sensu_enable_handlers: true

sensu_enable_haproxy_monitors: false
sensu_enable_process_monitors: true
sensu_enable_redis_monitors: false
sensu_handlers_dir: '{{ sensu_root_dir }}/handlers'

sensu_host: 'sensu.{{ sensu_pri_domain_name }}'

sensu_host_port: '4567'

# sensu_monitor_cpu:  #set enabled to either (y)es or (n)o below
#   - name: cpu
#     interval: 300
#     sub: ALL
#     enabled: true
#   - name: cpu_iowait
#     interval: 300
#     sub: ALL
#     enabled: true
# sensu_monitor_es: #set enabled to either (y)es or (n)o below
#   - name: cluster-status
#     interval: 60
#     sub: elasticsearch
#     enabled: true
#   - name: file-descriptors
#     interval: 60
#     sub: elasticsearch
#     enabled: true
#   - name: heap
#     interval: 60
#     sub: elasticsearch
#     enabled: false
# sensu_monitor_processes:  #set enabled to either (y)es or (n)o below
#   - name: apache
#     interval: 60
#     sub: apache
#     enabled: true
#   - name: cron
#     interval: 60
#     sub: ALL
#     enabled: true
#   - name: dhcpd
#     interval: 60
#     sub: dhcpd
#     enabled: true
#   - name: dnsmasq
#     interval: 60
#     sub: dnsmasq
#     enabled: true
#   - name: elasticsearch
#     interval: 60
#     sub: elasticsearch
#     enabled: true
#   - name: exim4
#     interval: 60
#     sub: exim4
#     enabled: true
#   - name: graylog
#     interval: 60
#     sub: graylog
#     enabled: true
#   - name: haproxy
#     interval: 60
#     sub: haproxy
#     enabled: true
#   - name: keepalived
#     interval: 60
#     sub: keepalived
#     enabled: true
#   - name: logstash
#     interval: 60
#     sub: logstash
#     enabled: true
#   - name: mongo
#     interval: 60
#     sub: mongodb
#     enabled: true
#   - name: mysql
#     interval: 60
#     sub: mysql
#     enabled: true
#   - name: nginx
#     interval: 60
#     sub: nginx
#     enabled: true
#   - name: pdns_server
#     interval: 60
#     sub: powerdns
#     enabled: true
#   - name: pdns_recursor
#     interval: 60
#     sub: powerdns
#     enabled: true
#   - name: rabbitmq
#     interval: 60
#     sub: rabbit
#     enabled: true
#   - name: redis
#     interval: 60
#     sub: redis
#     enabled: true
#   - name: rsyslogd
#     interval: 60
#     sub: ALL
#     enabled: true
#   - name: sensu-api
#     interval: 60
#     sub: sensu
#     enabled: true
#   - name: sensu-client
#     interval: 60
#     sub: ALL
#     enabled: true
#   - name: sensu-server
#     interval: 60
#     sub: sensu
#     enabled: true
#   - name: snmpd
#     interval: 60
#     sub: ALL
#     enabled: false
#   - name: squid
#     interval: 60
#     sub: squid
#     enabled: true
#   - name: sshd
#     interval: 60
#     sub: ALL
#     enabled: true
#   - name: uchiwa
#     interval: 60
#     sub: sensu
#     enabled: true
#   - name: zabbix_agentd
#     interval: 60
#     sub: ALL
#     enabled: false
# sensu_monitor_redis:
#   - name: ping
#     interval: 60
#     sub: redis
sensu_logstash_server_fqdn: 'logstash.{{ sensu_pri_domain_name }}'

# Defines the use of using multiple handlers if enable_handlers is true
# and more than one default_handler is required
sensu_multiple_handlers: true

sensu_plugins:
  - 'json'
  - 'mail'
  - 'redis'
  - 'rest-client'
  - 'sensu-plugin'
  - 'sensu-plugins-cpu-checks'
  - 'sensu-plugins-disk-checks'
  - 'sensu-plugins-memory-checks'
sensu_plugins_dir: '{{ sensu_root_dir }}/plugins'
sensu_pri_domain_name: 'example.org'

# Define RabbitMQ Info
sensu_rabbitmq_info:
  host: '{{ sensu_host }}'
  password: 'sensu'
  port: '5672'
  user: 'sensu'
  vhost: '/sensu'

sensu_redis_info:
  host: '{{ sensu_host }}'
  port: '6379'

sensu_root_dir: '/etc/sensu'

# Defines if host to be considered the sensu server
sensu_server: false

sensu_server_debian_packages:
  - build-essential
  - erlang-nox
  - mailutils
  - make
  - ruby2.3
  - ruby2.3-dev
  - sensu
  - uchiwa

sensu_server_services:
  - sensu-server
  - sensu-client
  - sensu-api
  - uchiwa

sensu_smtp_domain_name: '{{ sensu_pri_domain_name }}'
sensu_smtp_server: 'smtp.{{ sensu_pri_domain_name }}'
sensu_smtp_server_port: 25

sensu_uchiwa_info:
  host: '0.0.0.0'
  port: '3000'
  sensu_hosts:
    - host: '{{ sensu_host }}'
      # Define Datacenter name
      name: 'dc_1'
      port: '{{ sensu_host_port }}'
    # - host: '{{ sensu_host2 }}'
    #   name: 'sensu_host_2'
    #   port: '{{ sensu_host_port }}'
```

Dependencies
------------

https://github.com/RogersCompany/ansible-rabbitmq.git  
https://github.com/RogersCompany/ansible-redis.git  
https://github.com/RogersCompany/ansible-sensu.git  

Example Playbook
----------------

```
---
- hosts: sensu_server
  become: true
  vars:
    pri_domain_name: 'test.vagrant.local'
    sensu_client: false
    sensu_host: '127.0.0.1'
    sensu_server: true
  roles:
    - role: ansible-rabbitmq
    - role: ansible-redis
    - role: ansible-sensu
  tasks:

- hosts: sensu_clients
  become: true
  vars:
    pri_domain_name: 'test.vagrant.local'
    sensu_client: true
    sensu_host: '192.168.250.10'
    sensu_server: false
  roles:
    - role: ansible-sensu
      tags:
        - sensu_clients
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
[Sensu]: <https://sensuapp.org/>
