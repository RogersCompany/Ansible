# Role Name

An [Ansible](https://www.ansible.com) role to install/configure [Prometheus Node Exporter](https://github.com/prometheus/node_exporter)

## Requirements

None

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

None

## Example Playbook

```yaml
- hosts: all
  vars:
  roles:
    - role: ansible-prometheus-node-exporter
  tasks:
```

## License

MIT

## Author Information

Olivier ROGER

- [@RogersCompany](https://www.twitter.com/RogersCompany)
- [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
- [RogersCompany@gmail.com](mailto:RogersCompany@gmail.com)
