<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-docker](#ansible-docker)
  - [Build Status](#build-status)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-docker

An [Ansible](https://www.ansible.com) role to install/configure [Docker](https://www.docker.com)

## Build Status

[![Build Status](https://travis-ci.org/RogersCompany/ansible-docker.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-docker)

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-docker

# Ensure this exists if setting docker to alternate data directory
# We do not create this to ensure any add'l mounts do not overlay this path
# Service may fail to start if not.
docker_alt_data_dir: '/mnt/docker'

# Defines address of cluster address
# Not the same as Swarm Cluster address
# Ex. Consul
docker_cluster_addr: "{{ hostvars[inventory_hostname]['ansible_' + docker_cluster_interface]['ipv4']['address'] }}"

# Defines interface to capture address from for docker_cluster_addr
docker_cluster_interface: "{{ docker_swarm_interface }}"

docker_cluster_port: 2376

# Defines if docker should be configured to store data in alternate location
# ensure to enable -g option in docker_opts if true
docker_config_alt_data_dir: false

# Defines if docker service should be configured
docker_config_service: false

# Defines if users defined in docker_users should be added to docker group
docker_config_users: false

# Defines docker images to be installed
docker_images: []
  #   # Defines image name
  #   # ex. docker hub image name
  # - name: 'centos'
  #   # Defines state of image
  #   # present|absent
  #   state: 'present'
  # - name: 'elasticsearch'
  #   state: 'present'
  # - name: 'fedora'
  #   state: 'present'
  # - name: 'ubuntu'
  #   state: 'present'

# Defines if images defined in docker_images are managed
docker_manage_images: false

# Defines docker service options to be configured in /etc/docker/daemon.json
# Configure each option the same naming/format as the variables are set as at
# https://docs.docker.com/engine/reference/commandline/dockerd/
# The values are converted directly to proper JSON using the Jinja2 template
docker_opts:
# Only define bridge or bip if you want to use either one of these
# They cannot be used together
# Specify network bridge IP
  # bip: '172.17.0.1/8'
# Attach containers to a network bridge
  # bridge: 'docker0'
# Address or interface name to advertise
  # cluster-advertise: '{{ docker_cluster_addr }}:{{ docker_cluster_port }}'
# Set cluster store options
  # cluster-store: 'consul://192.168.250.10:8500'
# Enable debug mode
  debug: false
# Container default gateway IPv4 address
  # default-gateway: '10.10.10.1'
# Default ulimits for containers
  # default-ulimit:
  #   - nofile: '64000:64000'
# DNS server to use
  # dns:
  #   - '8.8.8.8'
  #   - '8.8.4.4'
# DNS search domains to use
  # dns-search:
  #   - 'etsbv.internal'
  #   - 'etsbv.test'
# Enable insecure registry communication
  # insecure-registries:
  #   - 'gitlab.etsbv.internal:5000'
# Default IP when binding container ports
  # ip: '0.0.0.0'
# Enable net.ipv4.ip_forward
  ip-forward: true
# Enable IP masquerading
  ip-masq: true
# Enable addition of iptables rules
  iptables: true
# Set key=value labels to the daemon
  # label:
  #   - environment: 'test'
  #   - datacenter: 'atlanta'
# Default driver for container logs
# Default is json-file
  log-driver: 'json-file'
# Fluentd log driver setup
  # log-driver: 'fluentd'
  # log-opts:
  #   fluentd-address: 'fluentdhost:24224'
  #   # fluentd-address: tcp://fluentdhost:24224
# End of Fluentd log driver setup
# GELF (Graylog) log driver setup
  # log-driver: 'gelf'
  # log-opts:
  #   gelf-address: 'udp://1.2.3.4:12201'
  #   tag: '{% raw %}{{.Name}}/{{.FullID}}{% endraw %}'
  #   labels: 'location'
  #   env: 'TEST'
# End of GELF (Graylog) log driver setup
# Splunk log driver setup
  # log-driver: 'splunk'
  # log-opts:
  #   splunk-token: '176FCEBF-4CF5-4EDF-91BC-703796522D20'
  #   splunk-url: 'https://splunkhost:8088'
  #   splunk-capath: '/path/to/cert/cacert.pem'
  #   splunk-caname: 'SplunkServerDefaultCert'
  #   tag: '{% raw %}{{.Name}}/{{.FullID}}{% endraw %}'
  #   labels: 'location'
  #   env: 'TEST'
# End of Splunk log driver setup
# Syslog log driver setup
  # log-driver: 'syslog'
  # log-opts:
  #   # Define syslog address or leave commented out for logging to host local
  #   # syslog.
  #   # syslog-address: 'udp://1.2.3.4:1111'
  #   tag: '{% raw %}{{.Name}}/{{.FullID}}{% endraw %}'
  #   labels: 'location'
  #   env: 'TEST'
# Set the logging level
  log-level: 'info'
# Set the max concurrent downloads for each pull
  max-concurrent-downloads: 3
# Set the max concurrent uploads for each push
  max-concurrent-uploads: 5
# Set the containers network MTU
  # mtu: 1500
# Enable selinux support
  selinux-enabled: false
# Storage driver to use
# aufs, devicemapper, btrfs, zfs, overlay and overlay2
  # storage-driver: 'aufs'
# Set default address or interface for swarm advertised address
  swarm-default-advertise-addr: "{{ docker_swarm_addr }}"
# Use TLS; implied by –tlsverify
  # tls: false

# Defines which repo to install from
# Stable gives you reliable updates every quarter
# Edge gives you new features every month
# define as stable or edge
docker_release_channel: 'stable'

# Defines if docker memory limits should be added to grub boot loader
docker_set_grub_memory_limit: true

docker_swarm_addr: "{{ hostvars[inventory_hostname]['ansible_' + docker_swarm_interface]['ipv4']['address'] }}"

docker_swarm_interface: 'enp0s8'

# Defines docker ubuntu repo info for installing from
docker_ubuntu_repo_info:
  id: '0EBFCD88'
  # keyserver: 'hkp://p80.pool.sks-keyservers.net:80'
  repo: 'deb [arch=amd64] https://download.docker.com/linux/{{ ansible_distribution | lower }} {{ ansible_distribution_release }} {{ docker_release_channel }}'
  url: 'https://download.docker.com/linux/ubuntu/gpg'

# Defines users to be added to docker group to allow non sudo access to docker
docker_users: []
  # - 'vagrant'

# Define Docker version to install
# 1.11.0|1.11.1|1.11.2|1.12.0|1.12.1|1.12.2|1.12.3|1.12.4|1.12.5|1.12.6|1.13.0|1.13.1
# 17.03.0|17.03.1|17.03.2|17.04.0|17.05.0|17.06.0
# Currently as of 06/03/2017 17.04.0 and 17.05.0 must be installed from the
# edge channel. Change docker_release_channel: 'edge'
docker_version: 17.06.0
```

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: docker_hosts
  vars:
    docker_swarm_interface: "eth1"
    docker_config_service: true
    pri_domain_name: 'test.vagrant.local'
  roles:
    - role: ansible-docker
  tasks:
```

## License

MIT

## Author Information

Olivier ROGER

-   [@RogersCompany](https://www.twitter.com/RogersCompany)
-   [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
-   [RogersCompany.com](http://RogersCompany.com)
-   RogersCompany [at] gmail.com
