# Role Name

An [Ansible] role to install/configure [fluentd]

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-fluentd
fluentd_debian_repo_info:
  repo: 'deb http://packages.treasuredata.com/2/{{ ansible_distribution|lower }}/{{ ansible_distribution_release|lower }}/ {{ ansible_distribution_release|lower }} contrib'
  repo_key: 'http://packages.treasuredata.com/GPG-KEY-td-agent'

fluentd_inputs: []
  # - type: 'tail'
  #   format: 'apache2'
  #   tag: 'apache.access'
  #   path: '/var/log/apache2/access.log'
  # - type: 'tail'
  #   format: '/^\[[^ ]* (?<time>[^\]]*)\] \[(?<level>[^\]]*)\] \[pid (?<pid>[^\]]*)\] \[client (?<client>[^\]]*)\] (?<message>.*)$/'
  #   tag: 'apache.error'
  #   path: '/var/log/apache2/error.log'
  # - type: 'syslog'
  #   port: 5140
  #   bind: 0.0.0.0
  #   tag: 'syslog'
  #   protocol_type: 'udp'
  # - type: 'tail'
  #   path: '/var/log/syslog'
  #   pos_file: '/var/log/syslog.pos'
  #   tag: 'syslog'
  #   format: 'syslog'

fluentd_network_optimizations:
  - name: 'net.ipv4.tcp_tw_recycle'
    state: 'present'
    value: 1
  - name: 'net.ipv4.tcp_tw_reuse'
    state: 'present'
    value: 1
  - name: 'net.ipv4.ip_local_port_range'
    state: 'present'
    value: '10240 65535'

fluentd_ouputs: []
  # - type: 'elasticsearch'
  #   logstash_format: true
  #   match: '**'
  #   host: '192.168.250.10'
  #   port: 9200
  #   index_name: 'fluentd'
  #   type_name: 'fluentd'
  # - type: 'rabbitmq'
  #   match: '**'
  #   host: 192.168.250.100
  #   user: 'graylog'
  #   pass: 'graylog'
  #   vhost: '/'
  #   format: 'json'
  #   exchange: 'graylog'
  #   exchange_type: 'direct'
  #   exchange_durable: true
  #   routing_key: 'graylog'
  #   heartbeat: 10

fluentd_plugins: []
  # - 'fluent-plugin-elasticsearch'
  # - 'fluent-plugin-rabbitmq'

fluentd_ulimits:
  - domain: 'root'
    limit_type: 'soft'
    limit_item: 'nofile'
    value: 65536
  - domain: 'root'
    limit_type: 'hard'
    limit_item: 'nofile'
    value: 65536
  - domain: '*'
    limit_type: 'soft'
    limit_item: 'nofile'
    value: 65536
  - domain: '*'
    limit_type: 'hard'
    limit_item: 'nofile'
    value: 65536
```

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: fluentd
  vars:
    fluentd_inputs:
      - type: 'tail'
        format: 'apache2'
        tag: 'apache.access'
        path: '/var/log/apache2/access.log'
      - type: 'tail'
        format: '/^\[[^ ]* (?<time>[^\]]*)\] \[(?<level>[^\]]*)\] \[pid (?<pid>[^\]]*)\] \[client (?<client>[^\]]*)\] (?<message>.*)$/'
        tag: 'apache.error'
        path: '/var/log/apache2/error.log'
      - type: 'syslog'
        port: 5140
        bind: 0.0.0.0
        tag: 'syslog'
        protocol_type: 'udp'
      - type: 'tail'
        path: '/var/log/syslog'
        pos_file: '/var/log/syslog.pos'
        tag: 'syslog'
        format: 'syslog'
    fluentd_ouputs:
      - type: 'elasticsearch'
        logstash_format: true
        match: '**'
        host: '192.168.250.10'
        port: 9200
        index_name: 'fluentd'
        type_name: 'fluentd'
    fluentd_plugins:
      - 'fluent-plugin-elasticsearch'
    pri_domain_name: 'test.vagrant.local'
  roles:
    - role: ansible-fluentd
```

## License

BSD

## Author Information

Olivier ROGER

-   [@RogersCompany]
-   <http://everythingshouldbevirtual.com>
-   RogersCompany [at] gmail.com

[@RogersCompany]: https://www.twitter.com/RogersCompany

[ansible]: https://www.ansible.com

[fluentd]: http://www.fluentd.org/
