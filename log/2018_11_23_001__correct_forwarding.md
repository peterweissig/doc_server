# 2018 11 22 ssl forwarding

[go back to server overview](../doc/server.md#ssl)

see also: [ssl forwarding](2018_11_22_001__added_ssl_forwarding.md)


## Info
Added forwarding from http:// to https://

Only changing "/etc/apache2/imscp/..." result in permament changes! \
Changed files within "/etc/apache2/sites-available/" will be resetted
by imscp.


## Problem
Previous redirect within /etc/apache2/imscp/... led to redirections
error.


## Reason
The regular (port 80) and the https (port 443) version of the website
include the imscp-files. Therefore the request redirected even if
already on https.


## Solution
Using if-condition.


## Steps

### 1. Edit conf-file

~~~~~
    $ cd /etc/apache2/imscp
    $ nano [[my_domain_name]].de.conf
        ... # Custom Apache configuration for [[my_domain_name]].de
        ... #
        ... # Any changes made to this file will be preserved on update.
        ... # i-MSCP doesn't checks the contents of this file.
        ... #
        ... # This file should NOT be deleted.
        >>>
        >>> # 2018 11 23 peter: added correct redirect for ssl
        >>> <If "%{HTTPS} == 'off'">
        >>>     Redirect permanent / https://[[my_domain_name]].de/
        >>> </If>
        >>>
~~~~~

### 2. Restart Apache

~~~~~
    $ service apache2 restart

    # old behaviour (bad)
    #    $ /etc/init.d/apache2 restart
~~~~~


## other
[abbreviations](../log/abbreviations.md)

