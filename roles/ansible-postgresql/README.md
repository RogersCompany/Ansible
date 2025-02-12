# Role Name

An [Ansible](https://www.ansible.com) role to install/configure [Postgresql](https://www.postgresql.org/)

## Requirements

Install [required](./requirements.yml) [Ansible] roles:

```bash
sudo ansible-galaxy install -r requirements.yml
```

If setting up replication:

`defaults/main.yml`

```yaml
# Define Ansible group which contains the hosts to setup replication
postgresql_replication_group: "postgres_replication"
```

## Role Variables

[Role Defaults](defaults/main.yml)

## Dependencies

None

## Example Playbook

[Example Playbook](./playbook.yml)

## License

MIT

## Author Information

Olivier ROGER

- [@RogersCompany](https://www.twitter.com/RogersCompany)
- [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
- [RogersCompany@gmail.com](mailto:RogersCompany@gmail.com)
