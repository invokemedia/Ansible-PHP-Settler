Ansible Laravel Homestead Settler
==================================

> Ansible scripts that build the Laravel Homestead development environment.

Originally forked from [konomae/ansible-laravel-settler](https://github.com/konomae/ansible-laravel-settler).

Requirements
------------

This role assumes you are using AWS EC2 and an external database like AWS RDS.

It installs PHP, PHP-FPM, and Nginx on the server. There are also flags to install [Redis](http://redis.io/), [Memcached](https://memcached.org/), [Beanstalkd](http://kr.github.io/beanstalkd/), and [Blackfire](https://blackfire.io/).

This role also assumes you are not going to be setting up more than 1 site on the server.

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
settler_nginx_default_server: default_server
settler_nginx_server_name: server_name
settler_nginx_site_folder_root: /var/www/laravel
```

Dependencies
------------

None.

Example Playbook
-------------------------

```
roles:
  - { role: invokemedia.ansible-laravel-settler }
```

License
-------

MIT

Author Information
------------------

* [Invoke Media](http://www.invokemedia.com/)
* <biz@invokemedia.com>

References
----------

* [laravel/homestead](https://github.com/laravel/homestead)
* [laravel/settler](https://github.com/laravel/settler)
