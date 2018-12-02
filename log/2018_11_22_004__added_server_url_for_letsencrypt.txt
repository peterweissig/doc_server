Problem:
    Direct access to main directory (/var/www/html) is not possible.
    But this is needed for letsencrypt to create a new certificate.

Solution:
    Added an other virtual host for alternativ server url.

###########################################################################

$ cd /etc/apache2/sites-available
$ nano <server_url>.conf
    # for added content see below

$ cd /etc/apache2/sites-enabled
$ ln -s ../sites-available/<server_url>.conf ./

###########################################################################
# file content

<VirtualHost <my_ip>:80>
    ServerAdmin webmaster@<server_url>
    ServerName <server_url>
    ServerAlias www.<server_url>
    DocumentRoot /var/www/html
    DirectoryIndex disabled
    LogLevel error
    ErrorLog /var/log/apache2/<server_url>/error.log
    <Directory /var/www/html>
        Options FollowSymLinks
        AllowOverride AuthConfig Indexes Limit Options=Indexes,MultiViews \
            Fileinfo=RewriteEngine,RewriteOptions,RewriteBase,RewriteCond,RewriteRule Nonfatal=Override
        Require all granted
    </Directory>

    #Redirect permanent / https://<server_url>/

</VirtualHost>

