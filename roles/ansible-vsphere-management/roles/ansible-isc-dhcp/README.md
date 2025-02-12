Role Name
=========

An [Ansible] role to install/configure [ISC-DHCP] server(s)

- Configurable options...failover and load balancing ready

[![Build Status](https://travis-ci.org/RogersCompany/ansible-isc-dhcp.svg)](https://travis-ci.org/RogersCompany/ansible-isc-dhcp)

Requirements
------------

For failover define the following vars to fit your deployment...
```
isc_dhcp_failover_info:
  failover_address: '{{ ansible_eth1.ipv4.address }}' #ansible_default_ipv4.address|ansible_enp0s8.ipv4.address #defines failover address for dhcp failover setup
  failover_group: 'dhcp-nodes'  #define Ansible inventory group that nodes belong to
  primary: 'node0'  #define the node in which should be considered the primary
  secondary: 'node1'  #define the node in which should be considered the secondary
```

Role Variables
--------------

```
---
# defaults file for ansible-isc-dhcp

# Defines if DHCP server should be authoritative for subnet
isc_dhcp_authoritative: false

# Defines if dhcp should be configured
isc_dhcp_config_dhcp: true

# Defines if ddns updates should be enabled between dhcp and dns
isc_dhcp_ddns_updates: false

# Defines ddns update style
# options are ad-hoc, interim, standard or none
# read more on this here
# https://deepthought.isc.org/article/AA-01091/0/ISC-DHCP-support-for-Standard-DDNS.html
isc_dhcp_ddns_update_style: 'none'

isc_dhcp_default_lease_time: 86400

# Define forward zones to forward to
isc_dhcp_dns_fwd_zones:
    #define forward zone name
  - zone: '{{ isc_dhcp_domain_name }}'
    #define forward zone primary dns server to forward to
    primary: '127.0.0.1'
isc_dhcp_dns_rev_zones:
    #define reverse zone
  - zone: '202.168.192'
    #define reverse zone primary dns server to forward to
    primary: '127.0.0.1'

# Defines domain name to assign to dhcp clients
isc_dhcp_domain_name: '{{ isc_dhcp_pri_domain_name }}'

# Defines if dhcp load balancing and failover should be configured
# between dhcp servers
isc_dhcp_enable_dhcp_failover: false

# Defines if TFTP/PXE boot options should be enabled
isc_dhcp_enable_pxe_boot: false

isc_dhcp_failover_info:
  # ansible_default_ipv4.address|ansible_enp0s8.ipv4.address
  # Defines failover address for dhcp failover setup
  failover_address: '{{ ansible_default_ipv4.address }}'
  # Define Ansible inventory group that nodes belong to
  failover_group: 'dhcp-nodes'
  # Define the node in which should be considered the primary
  primary: 'node0'
  # Define the node in which should be considered the secondary
  secondary: 'node1'

# Defines max lease time for clients
isc_dhcp_max_lease_time: 86400

# Defines dns servers to assign to dhcp clients
isc_dhcp_name_servers:
  - '8.8.8.8'
  - '8.8.4.4'

# Defines ntp servers for clients to poll
isc_dhcp_ntp_servers:
#  - 'ntp1.{{ isc_dhcp_pri_domain_name }}'
#  - 'ntp2.{{ isc_dhcp_pri_domain_name }}'
  - '0.ubuntu.pool.ntp.org'
  - '1.ubuntu.pool.ntp.org'

# Define global options to configure
isc_dhcp_options:
  - name: 'domain-name'
    value: '"{{ isc_dhcp_domain_name }}"'
  - name: 'domain-name-servers'
    value: '{{ isc_dhcp_name_servers|join (", ") }}'
  - name: 'ntp-servers'
    value: '{{ isc_dhcp_ntp_servers|join (", ") }}'

# Defines boot file used for pxe boot
isc_dhcp_pxe_boot_file: 'pxelinux.0'

# Defines tftp server to PXE/TFTP from
isc_dhcp_pxe_boot_server: 'tftp.{{ isc_dhcp_pri_domain_name }}'

# Defines dhcp scopes to create
isc_dhcp_scopes:
  - subnet: '192.168.202.0'
    default_lease_time: '{{ isc_dhcp_default_lease_time }}'
    max_lease_time: '{{ isc_dhcp_max_lease_time }}'
    netmask: '255.255.255.0'
    # Define scope specific options to configure
    options:
      - name: 'routers'
        value: '192.168.202.1'
      - name: 'subnet-mask'
        value: '255.255.255.0'
      - name: 'broadcast-address'
        value: '192.168.202.255'
      - name: 'domain-name-servers'
        value: '{{ isc_dhcp_name_servers|join (", ") }}'
    range: '192.168.202.128 192.168.202.224'

# Defines primary domain name for environment
isc_dhcp_pri_domain_name: 'example.org'
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
    - role: ansible-isc-dhcp
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
[ISC-DHCP]: <https://www.isc.org/downloads/dhcp/>
