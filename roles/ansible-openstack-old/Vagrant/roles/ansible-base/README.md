Role Name
=========

Common base role for all hosts. Should be ran after RogersCompany.bootstrap role.
(Configure update dhcp client,update dns servers,configure lvm)

[![Build Status](https://travis-ci.org/RogersCompany/ansible-base.svg?branch=master)](https://travis-ci.org/RogersCompany/ansible-base)
Requirements
------------

If creating, resizing or creating LVM volumes/volume groups ensure that you define the correct current disk and the new disk(s) added. If you choose to use apt-cacher ensure that you already have a server built and configured correctly for apt-caching.

Role Variables
--------------

````
---
# defaults file for ansible-base
config_monit: false  #defines if monit is to be configured if installed
install_monit: false  #defines if RogersCompany.monit role should be installed.
rundeck_generate_resources_xml: false  #defines if rundeck CI resources.xml should be generated if using rundeck...
rundeck_resources_xml_file: resources.xml  #defines the name of the resources file to be created on rundeck server
rundeck_resources_xml_location: /var/lib/rundeck/var  #defines defaults location on rundeck server to store the new resources.xml file
rundeck_server: []  #define server that is running rundeck CI if used...define here or globally in group_vars/all/servers
ssh_manage_ssh_known_hosts: false  #define if hosts ssh_known_hosts should be managed
update_dhcpclient_conf: false  #defines if dhcp client config should be updated...define here or globally in group_vars/all/configs
update_dns_nameservers: false  #defines if dns servers should be updated...define here or globally in group_vars/all/configs
update_dns_search: false  #defines if dns search domain should be updated...define here or globally in group_vars/all/configs
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
         - RogersCompany.base
#### GitHub
-----------
    - hosts: servers
      roles:
        - ansible-base

License
-------

BSD

Author Information
------------------

Olivier ROGER
- @RogersCompany
- http://everythingshouldbevirtual.com
- RogersCompany [at] gmail.com
