Role Name
=========

Installs plex server from https://plex.tv and sets up SMB mounts to media shares if desired.

Requirements
------------

None

Role Variables
--------------

````
---
# defaults file for ansible-plex
enable_firewall: false
plex_centos_file: 'plexmediaserver-{{ plex_version }}.x86_64.rpm'
plex_deb_file: 'plexmediaserver_{{ plex_version }}_amd64.deb'
plex_deb_url: '{{ plex_dl_url }}/{{ plex_deb_file }}'
plex_dl_dir: /opt  #define folder/dir to download plex to and install from
plex_dl_url: 'https://downloads.plex.tv/plex-media-server/{{ plex_version }}'
plex_mount_root: /media  #define the root folder where smb mounts should be created...
plex_mount_smb: false  #defines if mounting of smb shares is desired
plex_rpm_path: '/opt/{{ plex_version }}.rpm'
plex_smb_account: []
#  - user: ''  #define user name...defined in group_vars/all/accounts
#    domain: ''  #define domain if user is a domain account...defined in group_vars/all/accounts
#    passwd: ''  #define password for user...defined in group_vars/all/accounts
plex_smb_mounts: [] #define smb mounts to connect to on plex_smb_server...defined in group_vars/plex-servers
#  - movies
#  - music
#  - tv_shows
plex_smb_server: []  #define smb server to mount shares from...defined in group_vars/plex-servers
plex_version: '1.2.2.2857-d34b464'  #define version from https://plex.tv to download and install
````
Dependencies
------------

None

Example Playbook
----------------
#### Galaxy
-----------
    - hosts: servers
      roles:
         - { role: RogersCompany.plex }
#### GitHub
-----------
    - hosts: servers
      roles:
        - ansible-plex

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com
