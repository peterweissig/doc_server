Added forwarding from http:// to https://

Only changing "/etc/apache2/imscp/..." result in permament changes!
Changed files within "/etc/apache2/sites-available/" will be resetted
by imscp.

Problem:
    Previous redirect within /etc/apache2/imscp/... led to redirections
    error

Reason:
    The regular (port 80) and the https (port 443) version of the website
    include the imscp-files. Therefore the request redirected even if
    already on https.

Solution:
    Using if-condition

###########################################################################

$ cd /etc/apache2/imscp
$ nano <my_domain_name>.de.conf
    ... # Custom Apache configuration for <my_domain_name>.de
    ... #
    ... # Any changes made to this file will be preserved on update.
    ... # i-MSCP doesn't checks the contents of this file.
    ... #
    ... # This file should NOT be deleted.
    >>>
    >>> # 2018 11 23 peter: added correct redirect for ssl
    >>> <If "%{HTTPS} == 'off'">
    >>>     Redirect permanent / https://<my_domain_name>.de/
    >>> </If>
    >>>

$ /etc/init.d/apache2 restart


