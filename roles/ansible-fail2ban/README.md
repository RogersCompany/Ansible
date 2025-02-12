Role Name
=========

An [Ansible] role to install/configure [Fail2ban]

Requirements
------------

None

Role Variables
--------------

```
---
# defaults file for ansible-fail2ban

# Defines the length of time in seconds for which an IP is banned
fail2ban_bantime: '600'

fail2ban_chain: 'INPUT'

fail2ban_config: true

fail2ban_configs:
  - 'fail2ban.local'
  - 'jail.local'

# Set the file for the fail2ban persistent data to be stored
fail2ban_dbfile: '/var/lib/fail2ban/fail2ban.sqlite3'

# Sets age at which bans should be purged from the database
# Values: [ SECONDS ] Default: 86400 (24hours)
fail2ban_dbpurge_age: '86400'

# Defines the email address where you would like to receive the emails
fail2ban_destemail: 'root@localhost'

# Defines the length of time between login attempts before a ban is set
fail2ban_findtime: '600'

fail2ban_ignore_ips:
  - '127.0.0.1/8'
  - '10.0.0.0/8'

fail2ban_jails:
  # - jail: 'apache-auth'
  #   port:
  #     - 'http'
  #     - 'https'
  #   logpath: '%(apache_error_log)s'
  - jail: 'dropbear'
    port:
      - 'ssh'
    logpath: '%(dropbear_log)s'
  # - jail: 'squid'
  #   port:
  #     - '80'
  #     - '443'
  #     - '3128'
  #     - '8080'
  #   logpath: '/var/log/squid/access.log'
  - jail: 'sshd'
    port:
      - 'ssh'
    logpath: '%(sshd_log)s'
  - jail: 'sshd-ddos'
    port:
      - 'ssh'
    logpath: '%(sshd_log)s'
  # - jail: 'selinux-ssh'
  #   port:
  #     - 'ssh'
  #   logpath: '%(auditd_log)s'
  #   maxretry: '5'

# CRITICAL | ERROR | WARNING | NOTICE | INFO | DEBUG
fail2ban_log_level: 'INFO'

fail2ban_log_target: '/var/log/fail2ban.log'

# Defines How many attempts can be made to access the server from a
# single IP before a ban is imposed
fail2ban_maxretry: '3'

# Defines what mail service will be used to send mail
fail2ban_mta: 'sendmail'

# Set the PID file
fail2ban_pid_file: '/var/run/fail2ban/fail2ban.pid'

# Defines protocol types to filter
# tcp | udp | icmp | all
fail2ban_protocol: 'tcp'

# Defines the email address from which Fail2ban will send emails
fail2ban_sender: 'root@localhost'

# Defines the value of the "From" field in the email
fail2ban_sendername: 'Fail2ban'

# Set the socket file
fail2ban_socket: '/var/run/fail2ban/fail2ban.sock'
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-fail2ban
  tasks:
```

License
-------

BSD

Author Information
------------------
Olivier ROGER
- [@RogersCompany]
- [EverythingShouldBeVirtual]
- RogersCompany [at] gmail.com

[@RogersCompany]: <https://www.twitter.com/RogersCompany>
[EverythingShouldBeVirtual]: <http://www.everythingshouldbevirtual.com>

[Ansible]: <https://www.ansible.com>
[Fail2ban]: <https://www.fail2ban.org>
