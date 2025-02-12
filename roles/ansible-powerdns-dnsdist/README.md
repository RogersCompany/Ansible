<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Role Name](#role-name)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Role Name

An [Ansible](https://www.ansible.com) role to install [PowerDNS DNSDist](http://dnsdist.org/).

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-powerdns-dnsdist
pdns_dnsdist_config: true

pdns_dnsdist_acls:
  - 10.0.0.0/8
  # - 100.64.0.0/10
  - 169.254.0.0/16
  - 192.168.0.0/16
  - 172.16.0.0/12
  - ::1/128
  - fc00::/7
  - fe80::/10

pdns_dnsdist_cache:
  - name: pc
    # Required
    max_entries: 10000
    # Not required
    max_lifetime: 86400
    # Not required
    min_ttl: 0
    # Required...the default is blank as it creates a cache for the default pool
    # otherwise define a pool name
    pool: ""
    # Not required
    ttl_server_failure_response: 60
    # Not required
    ttl_stale_cache: 60

pdns_dnsdist_carbon_metrics_info:
  # Defines the interval in which to send metrics
  interval: 30
  # Defines the hostname which shows in metrics collection
  reporting_hostname: "{{ ansible_hostname }}"
  # Defines the server to send metrics to
  server: "graphite.{{ pdns_dnsdist_pri_domain_name }}"

pdns_dnsdist_debian_pre_reqs:
  - libsystemd-dev

pdns_dnsdist_debian_repo: "deb [arch=amd64] {{ pdns_dnsdist_repo_url }}/{{ ansible_distribution|lower }} {{ ansible_distribution_release|lower }}"
pdns_dnsdist_debian_repo_key: https://repo.powerdns.com/FD380FBB-pub.asc

# Defines domains in which to block inbound traffic from
pdns_dnsdist_domain_blocks:
  - ezdns.it.
  - sh43354.cn.

pdns_dnsdist_downstream_servers:
  # - address: 192.168.202.201
    # # Define order if order based selection is desired
    # order: 1
    # # Defines a pool name to assign the server to
    # pool: test
    # # Defines a different port for downstream server
    # port: 5300
    # # Defines the Queries Per Second limit
    # qps: 1000
    # # Defines receive timeout (default is 2)
    # recv_timeout: 2
    # # Defines send timeout (default is 2)
    # send_timeout: 2
  - address: 8.8.8.8
    pool: google
  - address: 8.8.4.4
    pool: google
  - address: 208.67.222.222
    pool: opendns
  - address: 208.67.220.220
    pool: opendns

# http://dnsdist.org/README/#acl-who-can-use-dnsdist
pdns_dnsdist_enable_acls: true

# http://dnsdist.org/README/#caching
pdns_dnsdist_enable_cache: true

# http://dnsdist.org/README/#carbongraphitemetronome
pdns_dnsdist_enable_carbon_metrics: false

pdns_dnsdist_enable_control_socket: true
pdns_dnsdist_enable_domain_blocks: false
pdns_dnsdist_enable_pool_rules: true

# http://dnsdist.org/README/#webserver
pdns_dnsdist_enable_webserver: true

pdns_dnsdist_local_address: 0.0.0.0

pdns_dnsdist_pool_rules: []
  # - query:
  #     - conviva.com
  #   pool: google
  # - query:
  #     - facebook.com.
  #   pool: opendns

pdns_dnsdist_pri_domain_name: example.org

pdns_dnsdist_redhat_pre_reqs:
  - epel-release
  - yum-plugin-priorities

pdns_dnsdist_repo_url: http://repo.powerdns.com

# firstAvailable|RoundRobin|whashed|wrandom|leastOutstanding
pdns_dnsdist_server_policy: leastOutstanding

# Make sure to change this key...generate a new one by running the following
# on your dnsdist server as I have not been able to get Ansible to automate
# the capturing of a generated key
# echo "makeKey()" | sudo dnsdist
pdns_dnsdist_setkey: "bKKPxcw4ieTkt29PenVFRcXzt1Nwc78TK+hHdUvqMCo="

# Define version to install...(1.0.x|1.1.x|1.2.x)
pdns_dnsdist_ver: 1.2.x

pdns_dnsdist_webserver_info:
  address: 0.0.0.0
  api_key: changeme
  port: 8083
  password: changeme
```

## Dependencies

None

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-powerdns-dnsdist
  tasks:
```

## License

BSD

## Author Information

Olivier ROGER

-   [@RogersCompany](https://www.twitter.com/RogersCompany)
-   [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
-   RogersCompany [at] gmail.com
