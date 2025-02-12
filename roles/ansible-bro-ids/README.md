# Role Name

An [Ansible] role to install/configure [BRO-IDS]

## Requirements

None

## Role Variables

    ---
    # defaults file for ansible-bro-ids
    bro_ids_criticalstack_intel_deb_repo_key: '{{ bro_ids_criticalstack_intel_url }}/gpgkey'

    bro_ids_criticalstack_intel_url: 'https://packagecloud.io/criticalstack/critical-stack-intel'

    bro_ids_debian_packages:
      - 'bro'
      - 'broctl'

    bro_ids_debian_pre_reqs:
      - 'apt-transport-https'
      - 'bison'
      - 'ca-certificates'
      - 'cmake'
      - 'curl'
      - 'debian-archive-keyring'
      - 'flex'
      - 'g++'
      - 'gcc'
      - 'libgeoip-dev'
      - 'libpcap-dev'
      - 'libssl-dev'
      - 'make'
      - 'python-dev'
      - 'swig'
      - 'zlib1g-dev'

    bro_ids_install_criticalstack: true

    bro_ids_listen_interface: 'enp0s3'

    # Location of other configuration files that can be used to customize
    # BroControl operation (e.g. local networks, nodes).
    bro_ids_broctl_cfg_dir: '/etc/bro'

    # Location of the log directory where log files will be archived each rotation
    # interval.
    bro_ids_broctl_log_dir: '/var/log/bro'

    # Expiration interval for log files in LogDir. Files older than this many days
    # will be deleted upon running "broctl cron".  A value of 0 means that logs
    # never expire.
    bro_ids_broctl_log_expire_interval: 0

    # Rotation interval in seconds for log files on manager (or standalone) node.
    # A value of 0 disables log rotation.
    bro_ids_broctl_log_rotation_interval: 3600

    # Mail connection summary reports each log rotation interval.  A value of 1
    # means mail connection summaries, and a value of 0 means do not mail
    # connection summaries
    bro_ids_broctl_mail_connection_summary: 1

    # Send mail when "broctl cron" notices the availability of a host in the
    # cluster to have changed.  A value of 1 means send mail when a host status
    # changes, and a value of 0 means do not send mail.
    bro_ids_broctl_mail_host_up_down: 1

    # Recipient address for all emails sent out by Bro and BroControl.
    bro_ids_broctl_mailto: 'root@localhost'

    # Lower threshold (in percentage of disk space) for space available on the
    # disk that holds SpoolDir. If less space is available, "broctl cron" starts
    # sending out warning emails.  A value of 0 disables this feature.
    bro_ids_broctl_min_disk_space: 5

    # Site-specific policy script to load. Bro will look for this in
    # $PREFIX/share/bro/site. A default local.bro comes preinstalled
    # and can be customized as desired.
    bro_ids_broctl_site_policy_standalone: 'local.bro'

    # Location of the spool directory where files and data that are currently being
    # written are stored.
    bro_ids_broctl_spool_dir: '/var/spool/bro'

    # Enable BroControl to write statistics to the stats.log file.  A value of 1
    # means write to stats.log, and a value of 0 means do not write to stats.log.
    bro_ids_broctl_stats_log_enable: 1

    # Number of days that entries in the stats.log file are kept.  Entries older
    # than this many days will be removed upon running "broctl cron".  A value of 0
    # means that entries never expire.
    bro_ids_broctl_stats_log_expire_interval: 0

    # Show all output of the broctl status command.  If set to 1, then all output
    # is shown.  If set to 0, then broctl status will not collect or show the peer
    # information (and the command will run faster).
    bro_ids_broctl_status_cmd_show_all: 1

    bro_ids_networks:
      - 10.0.0.0/8
      - 172.16.0.0/12
      - 192.168.0.0/16

    bro_ids_type: 'standalone'

## Dependencies

None

## Example Playbook

    - hosts: bro_ids
      vars:
      roles:
        - role: ansible-bro-ids
      tasks:

## License

BSD

## Author Information

Olivier ROGER

-   @RogersCompany
-   <http://everythingshouldbevirtual.com>
-   RogersCompany [at] gmail.com

[ansible]: https://www.ansible.com

[bro-ids]: https://www.bro.org/
