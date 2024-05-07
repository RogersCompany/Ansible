# ansible-snort

Installs and configures [Snort IDS](https://snort.org/)

## Requirements

None

## Vagrant

Spin up Environment under Vagrant to test.

```bash
vagrant up
```

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-snort
  tasks:
```

## License

MIT

## Author Information

Olivier ROGER

- [@RogersCompany](https://www.twitter.com/RogersCompany)
- [EverythingShouldBeVirtual](http://www.everythingshouldbevirtual.com)
- [RogersCompany@gmail.com](mailto:RogersCompany@gmail.com)