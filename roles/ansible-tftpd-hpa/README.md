# ansible-tftpd-hpa

An [Ansible](https://www.ansible.com) role to install/configure `tftpd-hpa`.

## Requirements

None

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: tftp_servers
  become: true
  vars:
  roles:
    - role: ansible-tftpd-hpa
  tasks:
```

## License

MIT

## Author Information

Olivier ROGER

- [@RogersCompany](https://www.twitter.com/RogersCompany)
- [EverythingShouldBeVirtual](http://www.everythingshouldbevirtual.com)
- [RogersCompany@gmail.com](mailto:RogersCompany@gmail.com)