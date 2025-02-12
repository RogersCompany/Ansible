Role Name
=========

An [Ansible] role to install/configure [Hashi-Vault]

Build Status
------------

[![Build Status](https://travis-ci.org/RogersCompany/ansible-hashi-vault.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-hashi-vault)

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-hashi-vault

# Defines the physical backend that Vault uses for storage
hashi_vault_backend: 'inmem'
hashi_vault_backend_listen_address: '127.0.0.1:8500'
hashi_vault_config: '/etc/vault.hcl'

hashi_vault_init_check_file: '/etc/.hashi_vault_initialized'

hashi_vault_init_output_file: '/etc/.hashi_vault_init.json'

hashi_vault_init_string:
  secret_shares: '{{ hashi_vault_secret_shares }}'
  secret_threshold: '{{ hashi_vault_secret_threshold }}'

hashi_vault_install_dir: '/usr/local/bin/'

# Defines one or more listeners determine how Vault listens for API requests
hashi_vault_listen_address: '127.0.0.1'

# Defines Vault listen port
hashi_vault_listen_port: '8200'

# Defines if vault secrets should be managed
hashi_vault_manage_secrets: false

# Defines if vault should be reinitialized
# this is only useful currently when using inmem as backend
hashi_vault_reinitialize: false

# Defines the number of secrets to generate
hashi_vault_secret_shares: 5

# Defines the threshold of the number of secrets required to unseal vault
hashi_vault_secret_threshold: 3

hashi_vault_secrets:
  - secret: 'hello'
    value: 'world'

# Defines if vault health status should be checked
hashi_vault_show_health_status: false

# Defines if vault key status should be checked
hashi_vault_show_key_status: false

# Defines if vault leader should be checked
hashi_vault_show_leader: false

# Defines if vault mounts should be checked
# lists all the mounted secret backends
hashi_vault_show_mounts: false

hashi_vault_tls_enabled: false
hashi_vault_url: 'https://releases.hashicorp.com'

hashi_vault_user_info:
  user: 'vault'
  group: 'vault'

hashi_vault_version: '0.7.0'
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: vault_servers
  become: true
  vars:
  roles:
    - role: ansible-hashi-vault
  tasks:
```

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com

[Ansible]: <https://www.ansible.com>
