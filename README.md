Ansible Laravel Homestead Settler
==================================

> Ansible scripts that build the Laravel Homestead development environment.

Originally forked from [konomae/ansible-laravel-settler](https://github.com/konomae/ansible-laravel-settler).

Requirements
------------

This role assumes you are using AWS EC2 and an external database like AWS RDS.

It installs PHP, PHP-FPM, and Nginx on the server. There are also flags to install [Redis](http://redis.io/), [Memcached](https://memcached.org/), [Beanstalkd](http://kr.github.io/beanstalkd/), and [Blackfire](https://blackfire.io/).

The role will also tweak [sysctl](https://linux.die.net/man/8/sysctl). We are using a config [from this site](https://easyengine.io/tutorials/linux/sysctl-conf/) to optimize the settings for a web server.

This role also assumes you are not going to be setting up more than 1 site on the server.

Installation
------------

`git clone https://github.com/invokemedia/ansible-laravel-settler roles/invokemedia.laravel-settler`

Role Variables
--------------

```
# update the cache?
settler_update_cache: yes
# cache timeout
settler_cache_valid_time: 3600

# flag for updating all the server packages
settler_upgrade_packages: yes

# file for timezone settings
#settler_timezone_file: /usr/share/zoneinfo/America/Vancouver
settler_timezone_file: /usr/share/zoneinfo/UTC

# the user for the system
settler_user: vagrant

# some additional tools
settler_redis: no
settler_memcached: no
settler_beanstalkd: no
settler_blackfire: no

# nginx settings
settler_nginx_default_server: 80
settler_nginx_server_name: localhost
settler_nginx_site_folder_root: /var/www/html/laravel
settler_nginx_site_public_folder: /public
```

Dependencies
------------

None.

Example Playbook
-------------------------

Here is how you would launch the default Nginx setup.

```
- hosts: web
  sudo: yes
  vars:
    settler_update_cache: no
    settler_upgrade_packages: no
    settler_nginx_site_folder_root: /var/www/html
    settler_nginx_site_public_folder: /public
  roles:
    - { role: invokemedia.laravel-settler }
```

You would need to have a project sent to `settler_nginx_site_folder_root` that contained a `/public` and then some index file inside that.

Handlers
--------

* `reload sysctl` - reload sysctl
* `restart nginx` - restarts nginx
* `restart php-fpm` - restarts php-fpm
* `restart memcached` - restarts memcached
* `restart beanstalkd` - restarts beanstalkd
* `restart blackfire-agent` - restarts blackfire-agent
* `restart redis-server` - restarts redis-server
* `set laravel folder permissions` - sets user and mode permissions on folders

License
-------

MIT

Author Information
------------------

* [Invoke Media](https://www.invokedigital.co/)
* <webmaster@invokedigital.co>

References
----------

* [laravel/homestead](https://github.com/laravel/homestead)
* [laravel/settler](https://github.com/laravel/settler)
