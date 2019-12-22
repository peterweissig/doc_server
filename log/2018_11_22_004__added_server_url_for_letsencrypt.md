# 2018 11 22 added server url for letsencrypt

[go back to server overview](../doc/server.md#letsencrypt)


## Problem
Direct access to main directory (/var/www/html) is not possible. \
But this is needed for letsencrypt to create a new certificate.


## Solution
Added an other virtual host for alternative server url.


## Steps

### 1. create new site

~~~~~
    $ cd /etc/apache2/sites-available
    $ nano [[server_url]].conf
        # for added content see below
~~~~~

### 2. enable new site

~~~~~
    $ a2ensite [[server_url]]

    # old behaviour (bad)
    #    $ cd /etc/apache2/sites-enabled
    #    $ ln -s ../sites-available/[[server_url]].conf ./
~~~~~


## file content

~~~~~
    <VirtualHost [[my_ip]]:80>
        ServerAdmin webmaster@[[server_url]]
        ServerName [[server_url]]
        ServerAlias www.[[server_url]]
        DocumentRoot /var/www/html
        DirectoryIndex disabled
        LogLevel error
        ErrorLog /var/log/apache2/[[server_url]]/error.log
        <Directory /var/www/html>
            Options FollowSymLinks
            AllowOverride AuthConfig Indexes Limit Options=Indexes,MultiViews \
                Fileinfo=RewriteEngine,RewriteOptions,RewriteBase,RewriteCond,RewriteRule Nonfatal=Override
            Require all granted
        </Directory>

        #Redirect permanent / https://[[server_url]]/

    </VirtualHost>
~~~~~


## other
[abbreviations](../log/abbreviations.md)
