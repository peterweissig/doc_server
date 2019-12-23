# 2019 update php

[go back to server overview](../doc/server.md#php)


## Info
https://tecadmin.net/switch-between-multiple-php-version-on-ubuntu/


## Steps

### 1. check version

~~~~~
    $ php --version
    $ ll /etc/alternatives | grep php
~~~~~


### 2. setup php-ppa
... todo ...

### 3. install php

~~~~~
    $ apt-get install php7.1 php7.1-dev php7.1-cgi
    $ apt-get install php7.1-common php7.1-curl php7.1-gd php7.1-gmp php7.1-imap \
    php7.1-intl php7.1-mbstring php7.1-mcrypt php7.1-mysql php7.1-pspell \
    php7.1-xml php7.1-zip
    $ apt-get install php-apcu php-symfony-polyfill-apcu php-imagick
~~~~~

### 4. setup apache

#### a) check version

~~~~~
    $ php --version

    $ ls /etc/apache2/mods-enabled/   | grep php
    $ ls /etc/apache2/mods-available/ | grep php
~~~~~

#### b) switch version
~~~~~
    $ a2dismod php7.0
    $ a2enmod  php7.1
    $ a2enconf php7.1-fpm
    $ a2enmod proxy_fcgi setenvif
~~~~~

#### php7.3

~~~~~
    $ a2dismod mpm_worker mpm_event
    $ a2enmod php7.3

    $ apt install php7.3-fpm
    $ a2enmod proxy_fcgi setenvif
    $ a2enconf php7.3-fpm

    $ service apache2 restart
~~~~~


### 5. update paths

~~~~~
    $ ll /etc/alternatives | grep php

    $ update-alternatives --list php
    $ update-alternatives --set php /usr/bin/php7.1
    $ update-alternatives --set php-cgi /usr/bin/php-cgi7.1
~~~~~


### 6. rerun imscp-config

~~~~~
    $ ~/install/imscp/1.5.3-20181208/engine/setup/imscp-reconfigure --reconfigure php
~~~~~
