# 2019 04 18 config php for nextcloud

[go back to nextcloud overview](../doc/nextcloud.md#php)


## Info
https://docs.nextcloud.com/server/15/admin_manual/installation/server_tuning.html#tune-php-fpm


## Steps
### 1. check current php version
see also [update php](2019__php_update.md)

~~~~~
    $ php --version

    $ ls /etc/apache2/mods-enabled/   | grep php
    $ ls /etc/apache2/mods-available/ | grep php
~~~~~

### 2. config php-fpm

~~~~~
    $ nano /etc/php/7.1/fpm/pool.d/www.conf
        # for added content see below
~~~~~


## file content

~~~~~
    [www]
    user = www-data
    group = www-data
    listen = /run/php/php7.1-fpm-www.sock
    listen.owner = www-data
    listen.group = www-data
    listen.mode = 0660

    # 2019 04 18 peter
    #    file:
    #        /etc/php/7.1/fpm/pool.d/www.conf
    #    based on this recommendation:
    #        https://docs.nextcloud.com/server/15/admin_manual/installation/server_tuning.html#tune-php-fpm
    #pm = ondemand
    #pm.max_children = 1
    pm.process_idle_timeout = 10s;
    pm.max_requests = 1000

    pm = dynamic
    pm.max_children = 120
    pm.start_servers = 12
    pm.min_spare_servers = 6
    pm.max_spare_servers = 18
~~~~~
