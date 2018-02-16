# Ansible Laravel Homestead Settler

Ansible scripts that build a Laravel Homestead-like environment.

_Originally forked from [konomae/ansible-laravel-settler](https://github.com/konomae/ansible-laravel-settler)._

## Requirements

This role installs PHP, PHP-FPM, and Nginx on the server. 

There are also optional services to install like:
 
- [Redis](http://redis.io/)
- [Memcached](https://memcached.org/)
- [Beanstalkd](http://kr.github.io/beanstalkd/)
- [Blackfire](https://blackfire.io/)

The role will also tweak [sysctl](https://linux.die.net/man/8/sysctl). 

We are using a config [from this site](https://easyengine.io/tutorials/linux/sysctl-conf/) to optimize the settings for a web server.

This role also assumes you are not going to be setting up more than 1 site on the server.

## Installation

`git clone https://github.com/invokemedia/ansible-laravel-settler roles/invokemedia.laravel-settler`

## Role Variables

```
# Add more public keys to the system?
add_ssh_users: false


# Auth file path, this is default:
ssh_auth_keys_file: "/home/{{ ansible_ssh_user }}/.ssh/authorized_keys"


# Update the cache?
settler_update_cache: yes


# Cache timeout
settler_cache_valid_time: 3600


# Flag for updating all the server packages
settler_upgrade_packages: yes


# File for timezone settings
settler_timezone_file: /usr/share/zoneinfo/America/Vancouver


# Timezone setting for PHP
settler_timezone: America/Vancouver


# the user for the system
settler_user: vagrant


# Optional installs
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

### Adding users for SSH access

You can add new users for SSH by setting `add_ssh_users` to `true` and then adding a `ssh_list` hash.

## Dependencies

None.

## Example Playbook

Here is how you would create a playbook to install a default nginx setup.

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

Example usage with a playbook:

```
ansible-playbook playbook.yml
```

You would need to have a project sent to `settler_nginx_site_folder_root` that contained a `/public` and then some index file inside that.

## Handlers

* `Reload sysctl` - reload sysctl
* `Restart nginx` - restarts nginx
* `Restart php-fpm` - restarts php-fpm
* `Restart memcached` - restarts memcached
* `Restart beanstalkd` - restarts beanstalkd
* `Restart blackfire-agent` - restarts blackfire-agent
* `Restart redis-server` - restarts redis-server
* `Set laravel folder permissions` - sets user and mode permissions on folders

## License

MIT

## Author

* [Invoke](https://www.invokedigital.co/)
* <webmaster@invokedigital.co>

## References

* [laravel/homestead](https://github.com/laravel/homestead)
* [laravel/settler](https://github.com/laravel/settler)
