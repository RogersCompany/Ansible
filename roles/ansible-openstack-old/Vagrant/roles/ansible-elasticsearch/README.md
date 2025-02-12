Role Name
=========

Installs elasticsearch role https://www.elastic.co/
######Configurable (cluster ready)

[![Build Status](https://travis-ci.org/RogersCompany/ansible-elasticsearch.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-elasticsearch)

Requirements
------------

None

Role Variables
--------------

````
---
# defaults file for ansible-elasticsearch
es_allow_remote_connections: false  #defines if remote connections should be allowed....version 2.x
es_cluster_name: ansible-test #defines es_cluster_name if not specified in group_vars
es_cluster_setup: false  #defines if elasticsearch will be setup as a cluster of nodes...define here or in group_vars/group
es_config_lvm: false  #defines if additional lvm volume is to be created
es_config_master_group: 'es-cluster-nodes'  #define inventory group to configure as master nodes..if same as es_config_unicast_group leave as is or change to another (ex.es-master-nodes)
es_config_nfs: false  #defines if an NFS mountpoint is to be mounted
es_config_path_data: false  #defines if elasticsearch should be configured to store data in different data paths
es_config_unicast: false  #defines if unicast discovery should be configured...ES 2.x
es_config_unicast_group: 'es-cluster-nodes'  #define inventory group to configure unicast discovery.
es_curator_close_after_days: 14  #defines the number of days before closing indexes
es_curator_max_keep_days: 30  #defines the max number of days to keep indexes
es_data_node: true  #defines if node should be a data node in the cluster...default is true...define here or in group_vars/group
es_debian_repo: 'deb http://packages.elastic.co/elasticsearch/{{ es_version }}/debian stable main'
es_disks:  #define disk device names to add to LVM VG if using
  - '/dev/sdb'
#  - '/dev/sdc'
es_docker_install: false  #defines if being installed in Docker
es_enable_network_tweaks: false  #defines if settings defined in es_network_tweaks are managed
es_fqdn: localhost
es_heap_size: '{{ (ansible_memtotal_mb | int * es_heap_size_multiplier) | round | int }}m'
#defines the amount of memory to allocate...Heap Size (defaults to 256m min, 1g max)...50% of max memory is good.
es_heap_size_multiplier: 0.5  #defines multiplier for determining the amount of memory to allocate to ES
es_lvextend_options: '-l +100%FREE'  #define options to pass to lvextend for extending LVM if used
es_lvname: elasticsearch-lv  #define LVM Logical Volume to create in VG Name if using
es_master_node: true  #defines if node should be a master node in the cluster...default is true...define here or in group_vars/group
es_memory_tuning:  #these settings help eliminate OOM conditions (More memory should be used in most cases but these settings can help) #define here or in group_vars/group
  - name: indices.breaker.fielddata.limit
    set: false
    value: 60%  #default 60%
  - name: indices.breaker.request.limit
    set: false
    value: 40%  #default 40%
  - name: indices.breaker.total.limit
    set: false
    value: 40%  #default 40%
  - name: indices.fielddata.cache.size
    set: false
    value: 40%  #default undefined
es_mntp: /var/lib/elasticsearch  #define mountpoint for LVM
#es_network_publish_host: []  #define a specific interface to bind elasticsearch on for clustering....usually not required...vagrant instances requires this...
es_network_tweaks:
  - name: 'net.ipv4.tcp_keepalive_time'
    state: present
    value: '600'
  - name: 'net.ipv4.tcp_keepalive_intvl'
    state: present
    value: '60'
  - name: 'net.ipv4.tcp_keepalive_probes'
    state: present
    value: '3'
es_nfs:
  - mount: []
    opts: defaults
    mountpoint: []
es_path_data_info:  #define disk devices and mountpoint path if elasticsearch should be configured to store data in different data paths
  - disk: /dev/sdc
    path: '{{ es_path_data_root }}/0'
  - disk: /dev/sdd
    path: '{{ es_path_data_root }}/1'
  - disk: /dev/sde
    path: '{{ es_path_data_root }}/2'
  - disk: /dev/sdf
    path: '{{ es_path_data_root }}/3'
  - disk: /dev/sdg
    path: '{{ es_path_data_root }}/4'
  - disk: /dev/sdh
    path: '{{ es_path_data_root }}/5'
es_path_data_root: /es_data  #defines root path for disks to be mounted if elasticsearch should be configured to store data in different data paths
es_plugin_bin: /usr/share/elasticsearch/bin/plugin
#es_plugin_install: -i  #define when ES vversion is below 2.x
es_plugin_install: install  #define when ES version is 2.x+
#es_plugin_list: -l  #define when ES version is below 2.x
es_plugin_list: list  #define when ES version is 2.x+
es_plugins_install:  #define plugins to install..naming is strange due to the way plugins are listed after installed
#  - plugin: elasticsearch/
#    name: marvel
#  - plugin: elastic/elasticsearch-
#    name: migration
#  - plugin: lukas-vlcek/
#    name: bigdesk
  - plugin: mobz/elasticsearch-
    name: head
  - plugin: royrusso/elasticsearch-
    name: hq
es_port: 9200
es_replicas: 1  #defines the number of replicas per shard in cluster...default is 1...define here or in group_vars/group
es_repo_key: 'https://packages.elastic.co/GPG-KEY-elasticsearch'
es_repo_url: 'http://packages.elastic.co/elasticsearch'
es_resize_lvm: false  #defines if lvm should be resized
es_shards: 5  #defines the number of primary shards per index...default is 5...define here or in group_vars/group
es_uninstall_plugins: false  #defines if installed plugins should be uninstalled...pass as cli var or other
es_vagrant_install: false  #defines if installing within a Vagrant environment
#es_version: 1.7
es_version: 2.x  #ready for 2.x release of Elasticsearch
es_vgname: elasticsearch-vg  #define LVM VG name if setting up lvm for elasticsearch data
install_bigdesk: true
install_curator: true
install_eshq: true
install_head: true
install_marvel: true
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
         - RogersCompany.elasticsearch
#### GitHub
-----------
    - hosts: servers
      roles:
        - ansible-elasticsearch

Docker Info
-----------

In order to run as a Docker container you will need to run the following (below example spins up a container named elasticsearch).
Ex.
````
docker run -d --name elasticsearch -p 9200:9200 RogersCompany/elasticsearch
````
You can change the name of the elasticsearch cluster (default is ansible-test) after the container is spun up if desired.
By executing the following:
````
docker exec -it elasticsearch ansible-playbook -i "localhost," -c local /opt/ansible-playbooks/playbook.yml --extra-vars="es_cluster_name=docker-es" && docker restart elasticsearch
````
The above will change the configuration for the elasticsearch cluster name and then the container is restarted.

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com
