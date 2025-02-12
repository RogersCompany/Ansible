Role Name
=========

An Ansible role to provision ELK Stack processors..

Requirements
------------

Install required Ansible roles...
````
ansible-galaxy install -r requirements.yml
````

Role Variables
--------------

````
---
# defaults file for ansible-elk-processors
alert_throttles:
  - tag: HardDrive-Failure
    settings:
      - name: period
        value: 300
      - name: before_count
        value: -1
      - name: after_count
        value: 1
      - name: key
        value: "%{host}%{message}"
clear_logstash_config: false
config_hosts_file: false  #defines if /etc/hosts should include ELK hosts...if DNS not configured...Vagrant testing.
config_logstash: true
email_notifications: 'notifications@{{ pri_domain_name }}'  #defines email address for logstash to send alerts to
enable_dns_blacklist_filtering: false  #defines if DNS blacklist filtering should be done...uncomment 361_filters_powerdns_blacklists under logstash_configs if set to true
enable_logstash_slack_output: false  #defines if logstash should be configured for sending alerts to slack
es_cluster_name: ansible-test #defines es_cluster_name if not specified in group_vars
esxinaming:  #define your VMware ESXi naming standards if used...this should be set to host pattern...example - esxi01.everythingshouldbevirtual.local - define as esxi
  - esxi
hadoopnaming: [] #define your Hadoop naming standards if used...this should be set to host pattern...example - hd01.everythingshouldbevirtual.local - define as hd
#  - hd  #uncomment and remove '' above if setting
logstash_alerts_domain: '{{ pri_domain_name }}'  #defines domain name to configure email alerts...generally should be the same as pri_domain_name
logstash_alerts_email: 'logstash_alerts@{{ pri_domain_name }}'  #defines email account to send alerts from
logstash_blacklists_dir: /etc/logstash/blacklists
logstash_config_dir: /etc/logstash/conf.d
logstash_log_dir: /var/log/logstash
logstash_configs:
  - pre_processor_000_inputs
  - pre_processor_001_filters
  - pre_processor_200_filters_syslog
  - pre_processor_210_filters_pfsense
  - pre_processor_220_filters_esxi
  - pre_processor_230_filters_vcenter
  - pre_processor_240_filters_quagga
  - pre_processor_999_outputs
  - processor_000_inputs
  - processor_001_filters
  - processor_100_filters_cisco_asa
  - processor_200_filters_syslog
  - processor_201_filters_monit
  - processor_210_filters_iptables
  - processor_220_filters_haproxy
  - processor_230_filters_keepalived
  - processor_240_filters_ssh
  - processor_241_filters_dhcp
  - processor_250_filters_snort
  - processor_260_filters_citrix_netscaler
  - processor_270_filters_apache
  - processor_280_filters_nginx
  - processor_290_filters_windows_eventlog
  - processor_300_filters_windows_updates
  - processor_310_filters_windows_iis
  - processor_320_filters_exim4
  - processor_330_filters_postfix
  - processor_340_filters_redis
  - processor_341_filters_rundeck
  - processor_350_filters_zfs
  - processor_360_filters_powerdns
#  - processor_361_filters_powerdns_blacklists
  - processor_370_filters_vmware_nsx
  - processor_900_filters
  - processor_910_filters_source_host_ip
  - processor_920_filters_alerting
  - processor_990_filters_cleanup
  - processor_991_filters_tagging
  - processor_999_outputs
logstash_configs_remove:  #define configs that were in logstash_configs but no longer needed below to remove them nodes. Move to logstash_configs to enable...
  - 000_inputs
  - 002_metrics  #comment out if metrics for logstash processing are not required..good for keeping track of throughput...removed because of incompatabilities w/ES 2.x
  - 101_filters_monit  #renamed to 201_filters_monit
  - 250_filters_vmware_nsx  #not working
  - 260_filters_mysql  #not working
  - 999_outputs
logstash_custom_tagging:  #Define ESXi, Hadoop, vCenter, Netscaler and etc type specific...replaces old naming methods. Uses DNS naming to define.
  - tag: 'ESXi'
    naming:
      - 'esxi'
      - 'ESXi'
#  - tag: 'Hadoop'
#    naming:
#      - 'hd-prod'
#      - 'hd-dev'
#  - tag: 'NSX'
#    naming:
#      - 'nsx-rt'
#      - 'vShield-edge'
  - tag: 'PFSense'
    naming:
      - 'pfsense'
  - tag: 'vCenter'
    naming:
      - 'vcsa'
#      - 'atl-vc'
#      - 'ny-vc'
logstash_custom_template: false  #defines if a custom elasticsearch template for logstash is desired.
logstash_file_inputs:
#  - path: /var/log/nginx/access.log
#    type: nginx-access
#  - path: /var/log/nginx/error.log
#    type: nginx-error
  - path: /var/log/mail.log
    type: postfix-log
#  - path: /var/log/redis/redis-server.log
#    type: redis-server
logstash_grok_patterns:
  - IPTABLES
  - NGINXERROR
logstash_pre_processor_inputs:
  - prot: tcp
    port: 10514
    type: syslog
#  - prot: tcp
#    port: 1514
#    type: VMware
#  - prot: tcp
#    port: 1515
#    type: vCenter
#  - prot: tcp
#    port: 1517
#    type: Netscaler
  - prot: tcp
    port: 28778
    type: elasticsearch-curator
  - prot: tcp
    codec: json
    port: 3515
    type: eventlog
#  - prot: tcp
#    codec: json_lines
#    port: 3525
#    type: iis
#  - prot: tcp
#    codec: json
#    port: '{{ rundeck_logstash_port }}'
#    type: rundeck
logstash_processor_inputs: []
#  - type: redis
#    batch_count: 1000
#    host: '127.0.0.1'
#    threads: 2
logstash_log_dir: /var/log/logstash
logstash_pre_processor_outputs: []
#  - output: redis
#    host: '127.0.0.1'
#  - output: rabbitmq
#    exchange: logstash
#    exchange_type: fanout
#    host: 10.0.101.128
logstash_processor_outputs:
  - output: elasticsearch
    hosts: '127.0.0.1:9200'
    protocol: http  #node, transport or http....http is the only protocol supported in 2.x+
    flush_size: 5000
    workers: 2
#  - output: gelf
#    host: 10.0.101.196
logstash_pre_tagging:
  - type: apache
    tags:
      - apache
  - type: eventlog
    tags:
      - WindowsEventLog
  - type: exim-log
    tags:
      - exim-log
  - type: iis
    tags:
      - IIS
  - type: logstash-log
    tags:
      - logstash-log
  - type: Netscaler
    tags:
      - Netscaler
  - type: nginx
    tags:
      - nginx
  - type: postfix-log
    tags:
      - postfix-log
  - type: redis-server
    tags:
      - redis-server
  - type: rundeck
    tags:
      - rundeck
  - type: snort
    tags:
      - snort
logstash_post_tagging:
  - type: ESXi
    tags:
      - VMware
  - type: NSX
    tags:
      - VMware
  - type: NSX-FW
    tags:
      - VMware
  - type: NSX-NAT
    tags:
      - VMware
  - type: vCenter
    tags:
      - VMware
logstash_server_fqdn: 'logstash.{{ pri_domain_name }}'  #defines logstash server...should be vip fqdn for elk-haproxy-nodes...define here or globally in group_vars/elk-nodes
logstash_slack_api_webhook_url: [] #define the slack api webhook api url assigned when adding an incoming slack webhook.
logstash_slack_channel: logstash  #defines the slack channel where logstash alerts should be sent to. Ensure enable_logstash_slack_output is set to true if slack output is required.
logstash_slack_output_tags:  #define specific tags to look for to alert on and send to slack
  - SSH_Failed_Login
#logstash_workers: 1  #defines the number of worker processes for logstash to spawn/cpu...default is 1/cpu...define here or in group_vars/group
powerdns_blacklists:
#  - malware
  - social_networking
  - spyware
pri_domain_name: example.org  #defines primary domain name...define here or globally in group_vars/all
skip_validation: true
smtp_server: 'smtp.{{ pri_domain_name }}'  #defines smtp server to send emails through...define here or globally in group_vars/all
````

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
    - role: ansible-elk-processors
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
