Role Name
=========

Installs and configures pacemaker and corosync http://clusterlabs.org/. Ability to configure cluster and define cluster settings. Ready for OpenStack..

Requirements
------------

None

Role Variables
--------------

````
---
# defaults file for ansible-pacemaker
corosync_bindnet_addr: "{{ ansible_eth1.ipv4.network }}"  #defines the interface to use for syncing cluster..this is a /24 address...ie...
corosync_expected_votes: 1  #defines the number of nodes to be functional in order to avoid split-brain scenarios...ex. 2-nodes = 1, 3-nodes = 2
last_man_standing: true  #Setting last_man_standing to true enables the Last Man Standing (LMS) feature; by default, it is disabled (set to false)
corosync_mcastaddr: 239.255.42.1  #define multicast address to use for cluster...this should be unique per cluster....
corosync_mcastport: 5405  #define port number to configure as cluster port.
corosync_start_service: "yes"
corosync_wait_for_all: true  #means that, When starting up a cluster (all nodes down), the cluster quorum is held until all nodes are online and have joined the cluster for the first time. This parameter is new in Corosync 2.0.
pacemaker_cluster_settings:  #define specific cluster settings to configure
  - property: pe-warn-series-max
    value: 1000
  - property: pe-input-series-max
    value: 1000
  - property: pe-error-series-max
    value: 1000
  - property: cluster-recheck-interval
    value: 5min
pacemaker_primary_server: false  #defines if host is considered to be primary....this should be set in host_vars/hostname as true for only one host
````

Dependencies
------------

None

Example Playbook
----------------

#### Galaxy
-----------
    - hosts: servers
      roles:
         - role: RogersCompany.pacemaker
#### GitHub
-----------
    - hosts: servers
      roles:
        - role: ansible-pacemaker

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com
