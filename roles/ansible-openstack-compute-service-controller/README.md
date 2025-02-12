<!-- START doctoc generated TOC please keep comment here to allow auto update -->

<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Table of Contents**  _generated with [DocToc](https://github.com/thlorenz/doctoc)_

-   [ansible-openstack-compute-service-controller](#ansible-openstack-compute-service-controller)
    -   [Requirements](#requirements)
    -   [Role Variables](#role-variables)
    -   [Dependencies](#dependencies)
        -   [Ansible Roles](#ansible-roles)
    -   [Example Playbook](#example-playbook)
    -   [License](#license)
    -   [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-openstack-compute-service-controller

An [Ansible](https://www.ansible.com) role to install/configure
[OpenStack Compute Service Controller](https://docs.openstack.org/ocata/install-guide-ubuntu/nova-controller-install.html)

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-openstack-compute-service-controller

# A list of APIs to enable by default
#
# ec2 is not available in Ocata
openstack_compute_service_controller_apis:
  # - ec2
  - metadata
  - osapi_compute

openstack_compute_service_controller_endpoint_services:
  - name: 'nova'
    type: 'compute'
    description: "Nova Service"
    api_port: 8774
    api_version: 'v2.1'
  - name: 'placement'
    type: 'placement'
    description: "Placement Service"
    api_port: 8778

# HA info
## Define as true if using HA
openstack_compute_service_controller_ha: false
## Define host which should be identified as HA master
openstack_compute_service_controller_ha_master: 'controller01'

# keystone_authtoken
openstack_compute_service_controller_keystone_authtoken:
  auth_type: 'password'
  auth_uri: '{{ openstack_compute_service_controller_keystone_service_endpoint_url }}:5000'
  auth_url: '{{ openstack_compute_service_controller_keystone_service_endpoint_url }}:35357'
  memcached_servers: '{{ openstack_compute_service_controller_memcached_servers }}'
  password: "{{ openstack_compute_service_controller_nova_user_info['password'] }}"
  project_domain_name: "{{ openstack_compute_service_controller_nova_user_info['domain_id'] }}"
  project_name: "{{ openstack_compute_service_controller_nova_user_info['project'] }}"
  user_domain_name: "{{ openstack_compute_service_controller_nova_user_info['domain_id'] }}"
  username: "{{ openstack_compute_service_controller_nova_user_info['name'] }}"

openstack_compute_service_controller_keystone_service_endpoint_region: 'RegionOne'
openstack_compute_service_controller_keystone_service_endpoint_url: 'http://{{ ansible_hostname }}'

# Management IP Info
openstack_compute_service_controller_management_interface: 'enp0s8'
openstack_compute_service_controller_management_ip: "{{ hostvars[inventory_hostname]['ansible_'+openstack_compute_service_controller_management_interface]['ipv4']['address'] }}"

# Define memcached servers
openstack_compute_service_controller_memcached_servers:
  - 127.0.0.1

# Neutron info
openstack_compute_service_controller_neutron:
  auth_type: 'password'
  auth_url: '{{ openstack_compute_service_controller_keystone_service_endpoint_url }}:35357'
  password: "{{ openstack_compute_service_controller_neutron_user_info['password'] }}"
  project_domain_name: "{{ openstack_compute_service_controller_neutron_user_info['domain_id'] }}"
  project_name: "{{ openstack_compute_service_controller_neutron_user_info['project'] }}"
  url: '{{ openstack_compute_service_controller_keystone_service_endpoint_url }}:9696'
  user_domain_name: "{{ openstack_compute_service_controller_neutron_user_info['domain_id'] }}"
  username: "{{ openstack_compute_service_controller_neutron_user_info['name'] }}"

# Define a suitable secret for the metadata proxy.
openstack_compute_service_controller_neutron_metadata_secret: []

# Neutron info
## Define Neutron user info
openstack_compute_service_controller_neutron_user_info:
  description: 'Neutron user'
  domain_id: 'default'
  enabled: true
  name: 'neutron'
  # Generate with openssl rand -hex 10
  password: '{{ openstack_compute_service_controller_neutron_user_pass }}'
  project: 'service'
  role: 'admin'
  state: 'present'

## Define Neutron user password
openstack_compute_service_controller_neutron_user_pass: []

# Nova DB info
openstack_compute_service_controller_nova_db_host: 'localhost'
openstack_compute_service_controller_nova_db_pass: 'nova'

# Nova info
## Define Nova user info
openstack_compute_service_controller_nova_user_info:
  description: 'Nova user'
  domain_id: 'default'
  enabled: true
  name: 'nova'
  # Generate with openssl rand -hex 10
  password: '{{ openstack_compute_service_controller_nova_user_pass }}'
  project: 'service'
  role: 'admin'
  state: 'present'

## Define Nova user password
openstack_compute_service_controller_nova_user_pass: []

# Placement info
openstack_compute_service_controller_placement:
  auth_type: 'password'
  auth_url: '{{ openstack_compute_service_controller_keystone_service_endpoint_url }}:35357/v3'
  password: "{{ openstack_compute_service_controller_placement_user_info['password'] }}"
  project_domain_name: "{{ openstack_compute_service_controller_placement_user_info['domain_id'] }}"
  project_name: "{{ openstack_compute_service_controller_placement_user_info['project'] }}"
  user_domain_name: "{{ openstack_compute_service_controller_placement_user_info['domain_id'] }}"
  username: "{{ openstack_compute_service_controller_placement_user_info['name'] }}"

## Placement user info
openstack_compute_service_controller_placement_user_info:
  description: 'Placement user'
  domain_id: 'default'
  enabled: true
  name: 'placement'
  # Generate with openssl rand -hex 10
  password: '{{ openstack_compute_service_controller_placement_user_pass }}'
  project: 'service'
  role: 'admin'
  state: 'present'

## Define placement user password
openstack_compute_service_controller_placement_user_pass: []

# RabbitMQ Connection Info
openstack_compute_service_controller_rabbit_hosts:
  - 127.0.0.1
openstack_compute_service_controller_rabbit_pass: 'openstack'
openstack_compute_service_controller_rabbit_user: 'openstack'

openstack_compute_service_controller_services:
  - name: 'nova'
    service_type: 'compute'
    description: 'OpenStack Compute'
    state: 'present'
  - name: 'placement'
    service_type: 'placement'
    description: 'OpenStack Placement API'
    state: 'present'

# Defines whether VNC is enabled or not
openstack_compute_service_controller_vnc: true
```

## Dependencies

### Ansible Roles

The following [Ansible](https://www.ansible.com) roles are required as part of
this role.

-   [ansible-chrony](https://github.com/RogersCompany/ansible-chrony)
-   [ansible-config-interfaces](https://github.com/RogersCompany/ansible-config-interfaces)
-   [ansible-etc-hosts](https://github.com/RogersCompany/ansible-etc-hosts)
-   [ansible-memcached](https://github.com/RogersCompany/ansible-memcached)
-   [ansible-mysql](https://github.com/RogersCompany/ansible-mysql)
-   [ansible-openstack-base](https://github.com/RogersCompany/ansible-openstack-base)
-   [ansible-openstack-identity-service](https://github.com/RogersCompany/ansible-openstack-identity-service)
-   [ansible-openstack-image-service](https://github.com/RogersCompany/ansible-openstack-image-service)
-   [ansible-openstack-openrc](https://github.com/RogersCompany/ansible-openstack-openrc)
-   [ansible-rabbitmq](https://github.com/RogersCompany/ansible-rabbitmq)

The above roles can be installed using `ansible-galaxy` along with [requirements.yml](./requirements.yml):

```bash
ansible-galaxy install -r requirements.yml
```

## Example Playbook

[Example Playbook](./playbook.yml)

## License

MIT

## Author Information

Olivier ROGER

-   [@RogersCompany](https://www.twitter.com/RogersCompany)
-   [EverythingShouldBeVirtual](http://www.everythingshouldbevirtual.com)
-   RogersCompany [at] gmail.com
