# Role Name

An [ansible] role to install/configure [dnsmasq]

## Build Status

[![Build Status](https://travis-ci.org/RogersCompany/ansible-dnsmasq.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-dnsmasq)

## Requirements

None

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
    - role: ansible-dnsmasq
  tasks:
```

## License

MIT

## Author Information

Olivier ROGER

-   [@RogersCompany]
-   <http://everythingshouldbevirtual.com>
-   RogersCompany [at] gmail.com

[@RogersCompany]: https://www.twitter.com/RogersCompany

[ansible]: https://ansible.com

[dnsmasq]: http://www.thekelleys.org.uk/dnsmasq/doc.html
