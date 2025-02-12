Role Name
=========

An [Ansible] role that installs/configures [phpIPAM]

- Options are in place for HA DB setup if desired.

Requirements
------------
Install required Ansible role dependencies...  
```
sudo ansible-galaxy install -r requirements.yml
```

Usage
-----

Logging into phpIPAM...  
http://iporhostname/phpipam/?page=login  

Default phpIPAM login is
```
admin/ipamadmin
```

Role Variables
--------------

```
---
# defaults file for ansible-phpipam
date: "{{ lookup('pipe', 'date +%Y%m%d-%H%M') }}"
enable_phpipam_db_backups: true

# Defines root of phpipam web
# If using http url headers...change this to '/'
phpipam_base: '/phpipam/'

phpipam_db_backup_name_prefix: 'phpipam_bkp'
phpipam_db_backup_root: '/backups/db/phpipam'

# Defines if backend db for pdns is clustered
phpipam_db_cluster: false

# Define db host
phpipam_db_host: 'localhost'

# Define db name
phpipam_db_name: 'phpipam'

# Define db password
phpipam_db_pass: phpipam

# Define db user
phpipam_db_user: phpipam

# Defines if cron jobs for scanning and etc. should be defined.
phpipam_define_cron_jobs: false

phpipam_download: 'https://sourceforge.net/projects/phpipam/files/{{ phpipam_download_file }}'
phpipam_download_file: 'phpipam-{{ phpipam_version }}.tar'

# Defines if phpIPAM is pulled from https://github.com/phpipam/phpipam to install
phpipam_install_from_git: true

 # Defines commit to checkout to install from..Helps keep consistent installs
 # Note - If not checking out master then the branch will be in a detached state
 # but will still allow changes to be made to configurations and such. Should not
 # cause any issues.
 # Examples
 # 9cbf625 Removed DHCP from settings
 # 861f98c Merge branch 'master' of https://github.com/phpipam/phpipam
 # 419aba5 Suppressed KEA arrors if cannot read leases file + shown error #777
# phpipam_install_git_version: '9cbf625'
phpipam_install_git_version: 'HEAD'
 # Change to HEAD to always checkout the latest

# Defines if current discovery functionality should be patched
phpipam_patch_discovery: false

# Defines if current email test functionality should be patched
phpipam_patch_email: false

phpipam_pre_load_db: true

# Defines if Apache2 should be configured in order to enable prettify links
phpipam_prettify_links: true

# Define if using a clustered mariadb mysql and define a single node as primary
phpipam_primary: 'node0'

# Defines the root folder of where phpipam is to be installed
phpipam_root: '{{ web_root }}/phpipam'
phpipam_timezone: 'America/New_York'

# Defines if phpipam is to be upgraded
phpipam_upgrade: false

# Defines the phpipam url to configure apache2 for if configured for url rewrite
phpipam_url: 'ipam.{{ pri_domain_name }}'

# Define phpipam version
# Only used when not installing via GIT.
# uses github .tar.gz file from https://github.com/phpipam/phpipam/releases
phpipam_version: '1.2'

# Defines the primary domain name
pri_domain_name: 'example.org'

web_root: '/var/www/html'
```

Dependencies
------------

Reference requirements section..

Example Playbook
----------------

````
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-apache2
    - role: ansible-mariadb-mysql
    - role: ansible-phpipam
````

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
[phpIPAM]: <http://phpipam.net/>
