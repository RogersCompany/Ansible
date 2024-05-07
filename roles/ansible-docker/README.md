<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

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

[defaults/main.yml](defaults/main.yml)

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

- [@RogersCompany](https://www.twitter.com/RogersCompany)
- [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
- [RogersCompany@gmail.com](mailto:RogersCompany@gmail.com)
