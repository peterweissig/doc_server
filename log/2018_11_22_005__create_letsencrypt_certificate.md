# 2018 11 22 create letsencrypt certificate

[go back to server overview](../doc/server.md#letsencrypt)


## Steps

### 1. Running Certbot for the first time.
run _certbot_

~~~~~
    $ certbot certonly
~~~~~

set all necessary settings

~~~~~
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

    >>> [[server_url]] www.[[server_url]]

        Obtaining a new certificate
        Performing the following challenges:
        http-01 challenge for [[server_url]]
        http-01 challenge for www.[[server_url]]
        Input the webroot for [[server_url]]: (Enter 'c' to cancel):

    >>> /var/www/html

        Select the webroot for www.[[server_url]]:
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
        /etc/letsencrypt/live/[[server_url]]/fullchain.pem
        Your key file has been saved at:
        /etc/letsencrypt/live/[[server_url]]/privkey.pem
        Your cert will expire on 2019-02-20. To obtain a new or tweaked
        version of this certificate in the future, simply run certbot
        again. To non-interactively renew *all* of your certificates, run
        "certbot renew"
        - If you like Certbot, please consider supporting our work by:

        Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
        Donating to EFF:                    https://eff.org/donate-le
~~~~~

### 2. Deactivate website afterwards

~~~~~
    $ a2dissite [[server_url]]
    $ service apache2 restart

    # old behaviour (bad)
    #    $ rm /etc/apache2/sites-enabled/[[server_url]].conf
    #    $ /etc/init.d/apache2 restart
~~~~~

### 3. Update certificates on imscp
_This is deprecated and was only needed for imscp._

~~~~~
    $ /var/www/imscp/engine/setup/imscp-reconfigure --reconfigure help
    $ /var/www/imscp/engine/setup/imscp-reconfigure --reconfigure panel_ssl
        # tons of questions ...
    $ /var/www/imscp/engine/setup/imscp-reconfigure --reconfigure services_ssl
        # tons of questions ...
~~~~~


## other
[abbreviations](../log/abbreviations.md)
