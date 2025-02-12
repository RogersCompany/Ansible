<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-nginx](#ansible-nginx)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-nginx

An [Ansible](https://www.ansible) role to install/configure [NGINX](http://nginx.org)

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-nginx
config_nginx: false
nginx_access_log: '/var/log/nginx/access.log'
nginx_enable_ipv6: false
nginx_enable_php: true
nginx_error_log: '/var/log/nginx/error.log'
nginx_events_block:
#  - 'multi_accept on'
  - 'worker_connections 768'

# Define any custom headers which you would like to have configured
nginx_headers: []
  # - 'set_real_ip_from 192.168.250.0/24'
  # - 'real_ip_header X-Real-IP'
  # - 'real_ip_recursive on'

nginx_http_block:
  basic_settings:
    - 'keepalive_timeout 65'
    - 'sendfile on'
#    - 'server_names_hash_bucket_size 64'
#    - 'server_name_in_redirect off'
#    - 'server_tokens off'
    - 'tcp_nodelay on'
    - 'tcp_nopush on'
    - 'types_hash_max_size 2048'
    - 'include /etc/nginx/mime.types'
    - 'default_type application/octet-stream'
  gzip_settings:
    - 'gzip on'
    - 'gzip_disable "msie6"'
#    - 'gzip_vary on'
#    - 'gzip_proxied any'
#    - 'gzip_comp_level 6'
#    - 'gzip_buffers 16 8k'
#    - 'gzip_http_version 1.1'
#    - 'gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript'
  logging_settings:
    - 'access_log {{ nginx_access_log }}'
    - 'error_log {{ nginx_error_log }}'
  vhost_configs:
    - 'include /etc/nginx/conf.d/*.conf'
    - 'include /etc/nginx/sites-enabled/*'
nginx_listen_port: 80
nginx_php_set_timezone: false
nginx_php_timezone: 'America/New_York'

# Defines settings added to /etc/nginx/sites-enabled/default
nginx_server_block:
  - server_name: 'localhost'
    default_server: true
    enable_php: true
    index:
      - 'index.php'
      - 'index.html'
      - 'index.htm'
    listen_address:
      - '*'
#      - '127.0.1.1'
    listen_port: '{{ nginx_listen_port }}'
    location: '/'
    root: '{{ nginx_web_root }}'
    try_files: '$uri $uri/ =404'
nginx_worker_processes: 4
```

## Dependencies

None

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-nginx
  tasks:
```

## License

MIT

## Author Information

Olivier ROGER

-   [@RogersCompany](https://www.twitter.com/RogersCompany)
-   [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
-   RogersCompany [at] gmail.com
