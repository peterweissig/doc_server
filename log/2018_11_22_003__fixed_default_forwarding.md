# 2018 11 22 default website

[go back to server overview](../doc/server.md#forwarding)


## Problem
Forwarding of not existing subdomain always goes to one specific subdomain.


## Reason
All not matched domains/subdomains default to first virtual-host
directive (e.g. blub.[[my_domain_name]].de ).

Files within apache config (/etc/apache2/sites-enabled) are processed
in alphabetical order. And therefore cloud.[[my_domain_name]].de is
processed before the main domain.


## Solution
Force processing of main domain before subdomains.


## Steps

~~~~~
    $ cd /etc/apache2/sites-enabled
    $ ln -s ../sites-available/[[my_domain_name]].de.conf     05_default.conf
    $ ln -s ../sites-available/[[my_domain_name]].de_ssl.conf 06_default_ssl.conf
~~~~~


## other
[abbreviations](../log/abbreviations.md)
