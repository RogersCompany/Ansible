Role Name
=========

An [Ansible] role to manage [iptables] firewall

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-iptables
iptables_chains:
  - name: 'DEFAULT-Allowed'
    rules:
      - comment: 'Allow SSH'
        ctstate: 'NEW'
        destination_port: '22'
        jump: 'LOGGING-Allowed'
        protocol: 'tcp'
        state: 'present'
        table: 'filter'
      - comment: 'Allow DHCP'
        ctstate: 'NEW'
        destination_port: '67:68'
        jump: 'LOGGING-Allowed'
        protocol: 'udp'
        state: 'present'
        table: 'filter'
  - name: 'INPUT'
    rules:
      - comment: 'Allow all established and related connections'
        ctstate: 'ESTABLISHED,RELATED'
        jump: 'LOGGING-Allowed'
        state: 'present'
        table: 'filter'
      - comment: 'Allow all connections from localhost to localhost'
        jump: 'LOGGING-Allowed'
        in_interface: 'lo'
        state: 'present'
        table: 'filter'
      - comment: 'Drop INVALID headers and checksums, invalid TCP flags, invalid ICMP messages and out of sequence packets'
        ctstate: 'INVALID'
        jump: 'DROP'
        state: 'present'
        table: 'filter'
      - comment: 'Allow ICMP for everything'
        ctstate: 'NEW'
        jump: 'LOGGING-Allowed'
        protocol: 'icmp'
        state: 'present'
        tables: 'filter'
      - comment: 'Allow SSH'
        destination_port: '22'
        jump: 'DEFAULT-Allowed'
        protocol: 'tcp'
        state: 'present'
        table: 'filter'
      - comment: 'Allow DHCP'
        destination_port: '67:68'
        jump: 'DEFAULT-Allowed'
        protocol: 'udp'
        state: 'present'
        table: 'filter'
  - name: 'LOGGING-Allowed'
    rules:
      - comment: 'Set logging limits'
        jump: 'LOG'
        limit: '2/min'
        state: 'present'
        table: 'filter'
      - comment: 'Allow and log'
        jump: 'ACCEPT'
        state: 'present'
        table: 'filter'
  - name: 'LOGGING-Dropped'
    rules:
      - comment: 'Drop and log'
        jump: 'LOG'
        limit: '2/min'
        state: 'present'
        table: 'filter'

# Define custom user-defined chains
iptables_custom_chains:
  - name: 'DEFAULT-Allowed'
    state: 'present'
  - name: 'ELK-RELATED-Allowed'
    state: 'present'
  - name: 'LOGGING-Allowed'
    state: 'present'
  - name: 'LOGGING-Dropped'
    state: 'present'

# Define default policies
iptables_default_policies:
  - name: 'INPUT'
    policy: 'ACCEPT'
  - name: 'FORWARD'
    policy: 'ACCEPT'
  - name: 'OUTPUT'
    policy: 'ACCEPT'

# Defines if user-defined chains should be flushed
iptables_flush_chains: false

# Defines if rules should be flushed
iptables_flush_rules: false

# Defines IP versions to define
iptables_enabled_versions:
  - 'v4'
#  - 'v6'

# Enable NAT Masquerading in order to share internet connection
iptables_nat_masquerade:
  enabled: false
  outbound_interface: 'eth0'
  inbound_interface: 'eth1'
  # source: ''

# Defines if rules should be persistent across reboots
iptables_persistent: true
iptables_save_file: '/etc/iptables.rules'
```

Dependencies
------------

None

Example Playbook
----------------

````
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-iptables
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

[Ansible]: <https://www.ansible.com>
[iptables]: <https://www.netfilter.org/>
