Role Name
=========

An [Ansible] role that Configures /etc/hosts

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-etc-hosts
# Defines if all nodes in play should be added to each hosts /etc/hosts
etc_hosts_add_all_hosts: false

# Defines if ipv6 info is included in /etc/hosts
etc_hosts_enable_ipv6: true

# Defines your primary dns suffix
etc_hosts_pri_dns_name: 'vagrant.local'

# Defines if node has static IP.
etc_hosts_static_ip: false

# Defines if ansible_host is used for defining hosts
etc_hosts_use_ansible_ssh_host: true

# Defines if ansible_default_ipv4.address is used for defining hosts
etc_hosts_use_default_ip_address: false
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
    - role: ansible-etc-hosts
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
