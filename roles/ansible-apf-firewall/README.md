Role Name
=========

Installs and configures APF Firewall (Advanced Policy Firewall)  
https://www.rfxn.com/projects/advanced-policy-firewall/

Requirements
------------

Installs requirements using Ansible Galaxy  
````
sudo ansible-galaxy install -r requirements.yml -f
````

Vagrant
-------

Spin up Vagrant environment  
````
vagrant up
````

Role Variables
--------------

````
---
# defaults file for ansible-apf-firewall
apf_firewall_all_stop: 'DROP'  # DROP | REJECT
apf_firewall_bfd_file: 'bfd-current.tar.gz'
apf_firewall_bfd_trig: 15  # how many failure events must an address have before being blocked?
apf_firewall_bfd_url: 'http://www.rfxn.com/downloads'
apf_firewall_allow_icmp_types_in:  #defines icmp types to allow ingress
  - 0
  - 11
  - 3
  - 30
  - 5
  - 8
apf_firewall_allow_tcp_ports_in:  #defines tcp ports to allow ingress
  - 22
#  - 80
apf_firewall_allow_udp_ports_in: ''  #defines udp ports to allow ingress
#  - 67
#  - 68
apf_firewall_devel_mode: false  #When set to enabled; 5 minute cronjob is set to stop the firewall
apf_firewall_iface_in: '{{ ansible_default_ipv4.interface }}'  #Untrusted Network interface(s)
apf_firewall_iface_out: '{{ ansible_default_ipv4.interface }}'  #Untrusted Network interface(s)
apf_firewall_iface_trusted: ''  #Trusted Network interface(s)
apf_firewall_install_path: '/etc/apf-firewall'
apf_firewall_log: '/var/log/apf_log'  #defines log file
apf_firewall_log_drop: false  # Log all traffic that is filtered by the firewall
apf_firewall_log_level: 'crit'  # What log level should we send all log data too?
apf_firewall_log_rate: 30  # Max firewall events to log per/minute.
apf_firewall_rab: false  #The use of RAB is such that it allows the firewall to track an address as it
# traverses the firewall rules and subsequently associate that address across
# any number of violations.
apf_firewall_rab_hitcount: 1  # This controls the amount of violation hits an address must have before it is blocked.
apf_firewall_rab_pscan_level: 2  # 0 = disabled | 1 = low security  | 2 = medium security | 3 = high security
apf_firewall_rab_timer: 300  # This is the amount of time (in seconds) that an address gets blocked
apf_firewall_set_addiface: false  #This feature firewalls any additional interfaces on the server as untrusted
apf_firewall_set_fast_load: false
apf_firewall_set_monokern: true  #allows apf firewall to run when kernel is not equal to 2.4.x or 2.6.x
apf_firewall_set_refresh: 10  #This controls how often, if at all, we want the trust system to refresh rules
apf_firewall_set_trim: 150  #This is the total amount of rules allowed inside of the deny trust system
apf_firewall_set_verbose: true
apf_firewall_set_vnet: false
apf_firewall_tcp_stop: 'DROP'  # RESET | DROP | REJECT
apf_firewall_udp_stop: 'DROP'  # RESET | DROP | REJECT | PROHIBIT
config_apf_firewall: true  #defines if apf_firewall should be configured based on above vars or leave default.
config_apf_firewall_bfd: true  #defines if brute force detection should be enabled
````

Dependencies
------------

None

Example Playbook
----------------

````
---
- name: Installs APF Firewall
  hosts: all
  become: true
  vars:
  roles:
    - role: ansible-apf-firewall
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
