2018 11 25 fixed mysql root login

[go back to imscp overview](../doc/imscp.md#mysql)


## Problem
Error for daily cron-job

~~~~~
    /etc/cron.daily/logrotate:
    ct to server at 'localhost' failed
    error: 'Access denied for user 'debian-sys-maint'@'localhost' (using password: YES)'
    error: error running shared postrotate script for '/var/log/mysql/mysql.log /var/log/mysql/mysql-slow.log /var/log/mysql/mariadb-slow.log /var/log/mysql/error.log '
    run-parts: /etc/cron.daily/logrotate exited with return code 1
~~~~~


## Solution
Update mysql password for system user.

See also https://i-mscp.net/thread/17241-daily-error-report-with-anacron/


## Steps

### 1. get current password

~~~~~
    $ cat /etc/mysql/debian.cnf
~~~~~

### 2. log into mysql and change privileges

~~~~~
    $ mysql
        >>> GRANT ALL PRIVILEGES ON *.* TO 'debian-sys-maint'@'localhost' IDENTIFIED BY '[[password]]' WITH GRANT OPTION;
        >>> GRANT ALL PRIVILEGES ON *.* TO 'debian-sys-maint'@'127.0.0.1' IDENTIFIED BY '[[password]]' WITH GRANT OPTION;
        >>> GRANT ALL PRIVILEGES ON *.* TO 'debian-sys-maint'@'::1' IDENTIFIED BY '[[password]]' WITH GRANT OPTION;
        >>> FLUSH PRIVILEGES;
        >>> \q
~~~~~

### 3. check login

~~~~~
    $ mysql -u debian-sys-maint -p[[password]]
        # exit with <strg>+<d>
~~~~~
