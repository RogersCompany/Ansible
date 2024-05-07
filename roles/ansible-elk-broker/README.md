Role Name
=========

Installs ELK Stack Role (ELK-Broker)

Requirements
------------

Prior to using this role you will want to add your nodes to the appropriate inventory group and create the corresponding group_vars/group with variables defined. You should create 3 elk-broker nodes. Examples below.
#####hosts inventory
````
[elk-nodes]
elk-broker-1
elk-broker-2
elk-broker-3

[elk-broker-nodes]
elk-broker-1
elk-broker-2
elk-broker-3

````

Role Variables
--------------

````
use_redis: true  #defines if redis is to be used for caching
use_rabbitmq: false  #defines if rabbitmq is to be used for caching
````

#####group_vars/elk-nodes
````
---
es_cluster_name: vagrant
es_cluster_setup: true
es_network_publish_host: _eth1:ipv4_
es_min_master_nodes: 2
redis_allow_remote_connections: true
````
#####group_vars/elk-broker-nodes
````
---
es_data_node: false
es_master_node: true
````

Dependencies
------------

````
RogersCompany.ntp
RogersCompany.rsyslog
RogersCompany.snmpd
RogersCompany.timezone
RogersCompany.rabbitmq, when: use_rabbitmq
RogersCompany.redis, when: use_redis
RogersCompany.elasticsearch
RogersCompany.elk-kibana
````

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: elk-broker-nodes
      roles:
        - RogersCompany.elk-broker
        - { role: RogersCompany.ntp }
        - { role: RogersCompany.rsyslog }
        - { role: RogersCompany.snmpd }
        - { role: RogersCompany.timezone }
        - { role: RogersCompany.redis, when: use_redis }
        - { role: RogersCompany.rabbitmq, when: use_rabbitmq }
        - { role: RogersCompany.elasticsearch }
        - { role: RogersCompany.elk-kibana }

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com
