1. Running Certbot for the first time.

2. Deactivate website afterwards.

3. Update certificates.

###########################################################################

$ certbot certonly

        How would you like to authenticate with the ACME CA?
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        1: Spin up a temporary webserver (standalone)
        2: Place files in webroot directory (webroot)
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Select the appropriate number [1-2] then [enter] (press 'c' to cancel):

    >>> 2<enter>

        Plugins selected: Authenticator webroot, Installer None
        Please enter in your domain name(s) (comma and/or space separated)  (Enter 'c'
        to cancel):

    >>> <my_server_name>.premium-vserver.net www.<my_server_name>.premium-vserver.net

        Obtaining a new certificate
        Performing the following challenges:
        http-01 challenge for <my_server_name>.premium-vserver.net
        http-01 challenge for www.<my_server_name>.premium-vserver.net
        Input the webroot for <my_server_name>.premium-vserver.net: (Enter 'c' to cancel):

    >>> /var/www/html

        Select the webroot for www.<my_server_name>.premium-vserver.net:
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        1: Enter a new webroot
        2: /var/www/html
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Select the appropriate number [1-2] then [enter] (press 'c' to cancel):

    >>> 2

        Waiting for verification...
        Cleaning up challenges

        IMPORTANT NOTES:
         - Congratulations! Your certificate and chain have been saved at:
           /etc/letsencrypt/live/<my_server_name>.premium-vserver.net/fullchain.pem
           Your key file has been saved at:
           /etc/letsencrypt/live/<my_server_name>.premium-vserver.net/privkey.pem
           Your cert will expire on 2019-02-20. To obtain a new or tweaked
           version of this certificate in the future, simply run certbot
           again. To non-interactively renew *all* of your certificates, run
           "certbot renew"
         - If you like Certbot, please consider supporting our work by:

           Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
           Donating to EFF:                    https://eff.org/donate-le


###########################################################################

$ rm /etc/apache2/sites-enabled/<my_server_name>.premium-vserver.net.conf
$ /etc/init.d/apache2 restart

###########################################################################

$ /var/www/imscp/engine/setup/imscp-reconfigure --reconfigure help
$ /var/www/imscp/engine/setup/imscp-reconfigure --reconfigure panel_ssl
    # tons of questions ...
$ /var/www/imscp/engine/setup/imscp-reconfigure --reconfigure services_ssl
    # tons of questions ...


