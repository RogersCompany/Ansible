Role Name
=========

Builds out a fully functional PXE/TFTP Server for OS deployments..
(Ubuntu included using Netboot)
Pre-Seed file template included and ESXi scripted install ready.

Requirements
------------

If ESXi scripted installs are needed you MUST upload the appropriate ISO's
to /var/lib/tftpboot/images and configure them in `defaults/main.yml`
```
tftpserver_vmware_iso_images:
  - file: VMware-VMvisor-Installer-6.0.0.update01-3029758.x86_64.iso
    folder: ESXi/6.0U1
```

Role Variables
--------------
```
---
# defaults file for ansible-tftpserver
tftpserver_apache_links:
  - 'ESXi_VIBS'
  - 'ESXi_boot'
  - 'images'
  - 'KS'
tftpserver_apache_root: '/var/www/html'
tftpserver_apt_cacher_server: 'apt-cache.{{ tftpserver_domain_name }}'

# Defines the mirror directory of webserver if using local apt repo mirror
# (apt-mirror) server.
tftpserver_apt_mirror_dir: '/ubuntu'
tftpserver_apt_mirror_server: 'apt-mirror.{{ tftpserver_domain_name }}'

# Define your local apt repo mirror (apt-mirror) server if you are using one.
tftpserver_bind_address: '{{ ansible_default_ipv4.address }}'

# Menu_default has been disabled to allow boot from local HD by default
tftpserver_boot_menu:
  - label: 'local'
    menu_label: '^Boot from hard drive'
    menu_default: true
    localboot: true
  # - label: 'install'
  #  menu_label: Install
  #  menu_default: false
  #  kernel: 'ubuntu-installer/amd64/linux'
  #  append: 'vga=788 initrd=ubuntu-installer/amd64/initrd.gz -- quiet'
  # - label: 'cli'
  #  menu_label: 'Command-line install'
  #  menu_default: false
  #  kernel: 'ubuntu-installer/amd64/linux'
  #  append: 'tasks=standard pkgsel/language-pack-patterns= pkgsel/install-language-support=false vga=788 initrd=ubuntu-installer/amd64/initrd.gz -- quiet'
  # - label: 'auto-install Ubuntu Netboot (Latest)'
  #   menu_label: 'Automated install Ubuntu (Latest)'
  #   menu_default: false
  #   kernel: 'ubuntu-installer/amd64/linux'
  #   append: 'auto=true priority=critical vga=788 initrd=tftp://{{ tftpserver_bind_address }}/ubuntu-installer/amd64/initrd.gz locale=en_US.UTF-8 kbd-chooser/method=us netcfg/choose_interface=auto url=tftp://{{ tftpserver_bind_address }}/preseed.cfg'
  # - label: 'CentOS 7 (Manual)'
  #   menu_label: 'CentOS 7 (Manual)'
  #   menu_default: false
  #   kernel: 'images/CentOS/7/images/pxeboot/vmlinuz'
  #   append: 'auto=true priority=critical vga=normal initrd=tftp://{{ tftpserver_bind_address }}/images/CentOS/7/images/pxeboot/initrd.img ip=dhcp inst.repo=http://{{ tftpserver_bind_address }}/images/CentOS/7'
  # - label: 'Ubuntu 12.04.5 (Manual)'
  #   menu_label: 'Install Ubuntu 12.04.5 (Manual)'
  #   menu_default: false
  #   kernel: 'images/Ubuntu/12.04/install/netboot/ubuntu-installer/amd64/linux'
  #   append: 'auto=true priority=critical vga=788 initrd=tftp://{{ tftpserver_bind_address }}/images/Ubuntu/12.04/install/netboot/ubuntu-installer/amd64/initrd.gz locale=en_US.UTF-8 kbd-chooser/method=us netcfg/choose_interface=auto live-installer/net-image=http://{{ tftpserver_bind_address }}/images/Ubuntu/12.04/install/filesystem.squashfs'
  # - label: 'Ubuntu 12.04.5 (Pre-Seed)'
  #   menu_label: 'Install Ubuntu 12.04.5 (Pre-Seed)'
  #   menu_default: false
  #   kernel: 'images/Ubuntu/12.04/install/netboot/ubuntu-installer/amd64/linux'
  #   append: 'auto=true priority=critical vga=788 initrd=tftp://{{ tftpserver_bind_address }}/images/Ubuntu/12.04/install/netboot/ubuntu-installer/amd64/initrd.gz locale=en_US.UTF-8 kbd-chooser/method=us netcfg/choose_interface=auto url=tftp://{{ tftpserver_bind_address }}/ubuntu_12.04_preseed.cfg live-installer/net-image=http://{{ tftpserver_bind_address }}/images/Ubuntu/12.04/install/filesystem.squashfs'
  # - label: 'Ubuntu 14.04.2 (Manual)'
  #   menu_label: 'Install Ubuntu 14.04.2 (Manual)'
  #   menu_default: false
  #   kernel: 'images/Ubuntu/14.04/install/netboot/ubuntu-installer/amd64/linux'
  #   append: 'auto=true priority=critical vga=788 initrd=tftp://{{ tftpserver_bind_address }}/images/Ubuntu/14.04/install/netboot/ubuntu-installer/amd64/initrd.gz locale=en_US.UTF-8 kbd-chooser/method=us netcfg/choose_interface=auto live-installer/net-image=http://{{ tftpserver_bind_address }}/images/Ubuntu/14.04/install/filesystem.squashfs'
  - label: 'Ubuntu 14.04.5 (Pre-Seed)'
    menu_label: 'Install Ubuntu 14.04.5 (Pre-Seed)'
    menu_default: false
    kernel: 'images/Ubuntu/14.04.5/install/netboot/ubuntu-installer/amd64/linux'
    append: 'auto=true priority=critical vga=788 initrd=tftp://{{ tftpserver_bind_address }}/images/Ubuntu/14.04.5/install/netboot/ubuntu-installer/amd64/initrd.gz locale=en_US.UTF-8 kbd-chooser/method=us netcfg/choose_interface=auto url=tftp://{{ tftpserver_bind_address }}/ubuntu_14.04.5_preseed.cfg live-installer/net-image=http://{{ tftpserver_bind_address }}/images/Ubuntu/14.04.5/install/filesystem.squashfs'
  - label: 'Ubuntu 16.04.1 (Pre-Seed)'
    menu_label: 'Install Ubuntu 16.04.1 (Pre-Seed)'
    menu_default: false
    kernel: 'images/Ubuntu/16.04.1/install/netboot/ubuntu-installer/amd64/linux'
    append: 'auto=true priority=critical vga=788 initrd=tftp://{{ tftpserver_bind_address }}/images/Ubuntu/16.04.1/install/netboot/ubuntu-installer/amd64/initrd.gz locale=en_US.UTF-8 kbd-chooser/method=us netcfg/choose_interface=auto url=tftp://{{ tftpserver_bind_address }}/ubuntu_16.04.1_preseed.cfg live-installer/net-image=http://{{ tftpserver_bind_address }}/images/Ubuntu/16.04.1/install/filesystem.squashfs'

# Defines if images folder(s) and isos should be added
tftpserver_build_images: true

# Defines if tftp services should be configured
tftpserver_config_tftp: true

tftpserver_domain_name: 'example.org'

# Defines if apt-cacher-ng is setup and added to preseed.cfg
tftpserver_enable_apt_caching: false

# Defines if using a local mirror (apt-mirror) and configures preseed.cfg
# as such. Do not use both apt_caching and apt_mirror...
tftpserver_enable_apt_mirror: false

# Define additional esxli commands to run in order to configure each host
tftpserver_esxi_addl_settings:
  - desc: 'Set default domain lookup name'
    command: 'esxcli network ip dns search add --domain={{ tftpserver_domain_name }}'
#  - desc: 'Add vmnic3 to vSwitch0'
#    command: 'esxcli network vswitch standard uplink add --uplink-name vmnic3 --vswitch-name vSwitch0'
#  - desc: 'SATP configurations'
#    commands:
#      - 'esxcli storage nmp satp set --satp VMW_SATP_SVC --default-psp VMW_PSP_RR'
#      - 'esxcli storage nmp satp set --satp VMW_SATP_DEFAULT_AA --default-psp VMW_PSP_RR'

# Defines if individual kickstart configs should be created
tftpserver_esxi_create_host_kickstart_configs: false
tftpserver_esxi_enable_snmp: false

# Defines if SSH and ESXi shell are to be enabled
tftpserver_esxi_enable_ssh_and_shell: false

# Defines if during TFTP/PXE load of ESXi hosts maintenance mode should be exited.
tftpserver_esxi_exit_maint_mode: false
tftpserver_esxi_global_network_options:
  - bootproto: 'dhcp'
    create_default_portgroup: false
    interface: 'vmnic0'
tftpserver_esxi_hosts: []
#  - name: 'esxi01'
#    bootproto: 'dhcp'
#    create_default_portgroup: false
#    interface: 'vmnic0'
#  - name: 'esxi02'
#    bootproto: 'static'
#    create_default_portgroup: false
#    interface: 'vmnic0'
#    ip: '10.0.106.22'
#    netmask: '255.255.255.0'
#    gateway: '10.0.106.1'
#    nameservers: ''

# Example options are... install --firstdisk=usb --overwritevmfs --novmfsondisk
# or ... install --firstdisk --overwritevmfs
tftpserver_esxi_install_disk_options: 'install --firstdisk --overwritevmfs'

tftpserver_esxi_install_vibs: false

# Define here or in group_vars/all/accounts (preferred)
tftpserver_esxi_root_pw: 'vmware1'

# Defines if tftpserver_esxi_root_pw has been set to an already encrypted password
tftpserver_esxi_root_pw_encrypted: false

tftpserver_esxi_snmp_options:
  - community: 'PUBLIC'
    allowed_from: '10.0.0.0/24'

tftpserver_esxi_vibs:
  - 'http://{{ ansible_fqdn }}/ESXi_VIBS/Dell/cross_oem-dell-openmanage-esxi_7.3.0.2.ESXi550-0000.vib'
  - 'http://{{ ansible_fqdn }}/ESXi_VIBS/Dell/cross_oem-dell-iSM-esxi_1.0.ESXi550-0000.vib'
  - 'http://{{ ansible_fqdn }}/ESXi_VIBS/PernixData/PernixData_bootbank_pernixcore-vSphere5.5.0_1.5.0.2-25498.vib'

tftpserver_images_folders:
  - 'CentOS/7'
  # - 'ESXi/5.1'
  # - 'ESXi/5.1U1'
  # - 'ESXi/5.1U2'
  # - 'ESXi/5.5'
  # - 'ESXi/5.5U1'
  # - 'ESXi/5.5U2'
  - 'ESXi/5.5U3'
  # - 'ESXi/6.0'
  - 'ESXi/6.0U1'
  # - 'Ubuntu/12.04'
  - 'Ubuntu/14.04'
  - 'Ubuntu/16.04'

# Define ISO images to download
tftpserver_iso_images: []
#  - url: 'http://www.gtlib.gatech.edu/pub/centos/7/isos/x86_64'
#    file: 'CentOS-7-x86_64-Minimal-1503-01.iso'
#    folder: 'CentOS/7'
#  - url: 'http://mirror.pnl.gov/releases/12.04'
#    file: 'ubuntu-12.04.5-server-amd64.iso'
#    folder: 'Ubuntu/12.04'
#  - url: 'http://mirror.pnl.gov/releases/14.04'
#    file: 'ubuntu-14.04.2-server-amd64.iso'
#    folder: 'Ubuntu/14.04'
  - url: 'http://mirrors.kernel.org/ubuntu-releases/14.04'
    file: 'ubuntu-14.04.5-server-amd64.iso'
    folder: 'Ubuntu/14.04.5'
  - url: 'http://mirrors.kernel.org/ubuntu-releases/16.04'
    file: 'ubuntu-16.04.1-server-amd64.iso'
    folder: 'Ubuntu/16.04.1'

tftpserver_netboot_file: 'netboot.tar.gz'
tftpserver_netboot_url: 'http://archive.ubuntu.com/ubuntu/dists/trusty-updates/main/installer-amd64/current/images/netboot'

# Defines if custom partitioning is required
tftpserver_preseed_expert_recipe_partitioning: false

# Define the partitions to create during pre-seed
tftpserver_preseed_expert_recipe_partitions:
  - name: 'boot'
    mountpoint: '/boot'
    bootable: true
    filesystem: 'ext4'
    # This is an example only for /boot  do not assign an lv_name for boot
    # .boot will not be part of LVM.
    # lv_name: boot
    max_size: '1000'
    method: 'format'
    min_size: '500'
    priority: '50'
    use_filesystem: true
  - name: 'swap'
    # mountpoint:  #not needed for swap
    # bootable: false  #not needed for swap.
    filesystem: 'linux-swap'
    # Defines the LVM name to use if
    # tftpserver_preseed_partitioning_method: lvm and
    # tftpserver_preseed_expert_recipe_partitioning: true
    lv_name: 'swap'
    max_size: '2048'
    method: 'swap'
    min_size: '500'
    priority: '512'
    # use_filesystem: true
  - name: 'root'
    mountpoint: '/'
    # bootable: false  #not needed for root
    filesystem: 'ext4'
    # Defines the LVM name to use if
    # tftpserver_preseed_partitioning_method: lvm and
    # tftpserver_preseed_expert_recipe_partitioning: true
    lv_name: 'root'
    max_size: '10000'
    method: 'format'
    min_size: '5000'
    priority: '10000'
    use_filesystem: true

# Defines preseed.cfg to generate
tftpserver_preseed_files:
  - distro: 'ubuntu'
    version: '12.04.5'
  - distro: 'ubuntu'
    version: '14.04.5'
  - distro: 'ubuntu'
    version: '16.04.1'

# Define mirror...(us.archive.ubuntu.com)
tftpserver_preseed_mirror: '{{ ansible_hostname }}'

# Define mirror...(us.archive.ubuntu.com)
tftpserver_preseed_mirror_hostname: '{{ ansible_hostname }}'

# Defines if system clock is synced from NTP during install
tftpserver_preseed_ntp_sync: true

# Define packages to install during pre-seed installation(s)
tftpserver_preseed_packages:
  - 'openssh-server'
  # - 'open-vm-tools'

# Defines disk to install to during pre-seed TFTP/PXE install
tftpserver_preseed_partition_disk: '/dev/sda'

# Defines partitioning method....lvm, regular or crypto
tftpserver_preseed_partitioning_method: 'lvm'

# Defines if host should be shutdown after installing
# good for mass PXE deployments when the option to do a one-time boot to
# PXE is not an option.
tftpserver_preseed_poweroff_after_install: false

# To generate passwords use (replace P@55w0rd with new password)
# echo "P@55w0rd" | mkpasswd -s -m sha-512
# Define password as encrypted password and set encrypted_password=true
tftpserver_preseed_user_info:
  # Defines if password has been entered as encrypted or not
  encrypted_password: false
  full_username: 'Ubuntu User'
  password: 'ubuntu'
  # Defines if password prompt for sudo
  sudo_password: true
  username: 'ubuntu'
tftpserver_tftpboot_dir: '/var/lib/tftpboot'
tftpserver_vmware_iso_images: []
#  - file: VMware-VMvisor-Installer-6.0.0.update01-3029758.x86_64.iso
#    folder: ESXi/6.0U1
```

Dependencies
------------
Install the required Ansible roles by running:
`ansible-galaxy install -r requirements.yml`

Example Playbook
----------------

```
---
- hosts: all
  become: true
  vars:
    dnsmasq_config: true
    dnsmasq_dhcp_boot: 'pxelinux.0,{{ inventory_hostname }},{{ dnsmasq_pri_bind_address }}'
    dnsmasq_dhcp_scopes:
      - start: '192.168.250.128'
        end: '192.168.250.224'
        netmask: '255.255.255.0'
    dnsmasq_dhcp_options:
      - option: 'dns-server'
        value:
          - '192.168.250.10'
          # - '192.168.250.201'
      # - option: 'domain-name'
      #   value:
      #     - 'another.{{ dnsmasq_pri_domain_name }}'
      - option: 'domain-search'
        value:
          - 'dev.{{ dnsmasq_pri_domain_name }}'
          - 'prod.{{ dnsmasq_pri_domain_name }}'
          - 'test.{{ dnsmasq_pri_domain_name }}'
      - option: 'ntp-server'
        value:
          - '192.168.250.10'
          # - '192.168.250.201'
      - option: 'router'
        value:
          - '192.168.250.1'
    # Defines if DHCP services are provided by DNSMASQ
    dnsmasq_enable_dhcp: false
    # Defines if TFTP services are provided by DNSMASQ
    dnsmasq_enable_tftp: true
    dnsmasq_pri_bind_address: '{{ ansible_enp0s8.ipv4.address }}'
    dnsmasq_pri_domain_name: '{{ pri_domain_name }}'
    etc_hosts_add_all_hosts: true
    isc_dhcp_authoritative: true
    isc_dhcp_scopes:
      - subnet: '192.168.250.0'
        default_lease_time: '{{ isc_dhcp_default_lease_time }}'
        max_lease_time: '{{ isc_dhcp_max_lease_time }}'
        netmask: '255.255.255.0'
        # Define scope specific options to configure
        options:
          - name: 'routers'
            value: '192.168.250.1'
          - name: 'subnet-mask'
            value: '255.255.255.0'
          - name: 'broadcast-address'
            value: '192.168.250.255'
          - name: 'domain-name-servers'
            value: '{{ isc_dhcp_name_servers|join (", ") }}'
        range: '192.168.250.128 192.168.250.224'
    # Defines primary domain name for environment
    isc_dhcp_pri_domain_name: '{{ pri_domain_name }}'
    # Defines if TFTP/PXE boot options should be enabled
    isc_dhcp_enable_pxe_boot: true
    # Defines boot file used for pxe boot
    isc_dhcp_pxe_boot_file: 'pxelinux.0'
    # Defines tftp server to PXE/TFTP from
    isc_dhcp_pxe_boot_server: '192.168.250.10'
    pri_domain_name: 'test.vagrant.local'
    tftpserver_bind_address: '{{ ansible_enp0s8.ipv4.address }}'
  roles:
    - role: ansible-etc-hosts
    - role: ansible-dnsmasq
    - role: ansible-isc-dhcp
    - role: ansible-tftpserver
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
