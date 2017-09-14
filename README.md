ansible-role-craft
=====

This role quickly setup a Craft CMS project.
It download and install all dependencies for related project.

[![Ansible Galaxy](https://img.shields.io/badge/style-plumelo.craft-blue.svg?style=flat&label=role&test=plumelo.craft)](https://galaxy.ansible.com/plumelo/craft/)

Requirements
------------
This role requires Ansible 2.3.

Install
-------
```sh
ansible-galaxy install plumelo.craft
```
Role Variables
--------------
The variables that can be passed to this role and a brief description about them are as follows. (For all variables, take a look at defaults/main.yml)

```yaml
# prerequisites for clone, build, unzip, permissions, memory cache
craft_pkgs:
  - git
  - build-essential
  - zip
  - unzip
  - acl
  - memcached
```
```yaml
# project name, craft user
craft_name: project_name
craft_user: '{{ craft_name }}'
```
```yaml
# install php
craft_php_packages:
  - php7.1-fpm
  - php-mysql
  - php-mcrypt
  - php-mbstring
  - php-memcached
  - php-curl
  - php-gd
  - php-zip
  - php-readline
```
```yaml
# configure php-fpm
_craft_fpm_settings:
  name: '{{ craft_name }}'
  listen: '/var/run/fpm.{{ craft_name }}.socket'
  user: '{{ craft_user }}'
  group: '{{ craft_user }}'
  listen.owner: www-data
  listen.group: www-data
  chdir: /
```
```yaml
# install and configure mysql
craft_mysql_install: true
craft_db_name: '{{ craft_name }}'
craft_db_user: '{{ craft_name }}'
craft_db_pass: '{{ craft_db_user }}'
craft_db_path:
```
```yaml
# install and configure nginx
craft_nginx_install: true
_craft_nginx_site:
  template: 'craft.conf.j2'
  server_name: '{{ craft_name }}.local'

craft_nginx_site: {}
craft_nginx_sites:
  '{{ craft_name }}': '{{ _craft_nginx_site| combine(craft_nginx_site) }}'
```

Examples
--------
```yaml
- hosts: all
  vars:
    - craft_name: project_name
    - craft_path: /srv
    - craft_user: admin
    - craft_repo: git@github.com:project/project.git
    - craft_db_name: '{{ craft_name }}'
    - craft_db_user: '{{ craft_name }}'
    - craft_db_pass: '{{ craft_db_user }}'
  roles:
    - role: plumelo.craft
```

Dependencies
------------
```yaml
roles:
  - nbz4live.php-fpm
  - megheaiulian.mysql
  - jdauphant.nginx
  - plumelo.nginx_src
```
Licence
-------
BSD

Author Information
------------------
plumelo.com
