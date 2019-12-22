# 2018 11 22 ssl forwarding

[go back to server overview](../doc/server.md#ssl)

see also: [correct ssl forwarding](2018_11_23_001__correct_forwarding.md)


## Info
Added forwarding from http:// to https://

Only changing files within "/etc/apache2/sites-available/" can be used. \
Changes to "/etc/apache2/imscp/" result in an error!


## Steps
Editing domain

~~~~~
    $ cd /etc/apache2/sites-available
    $ nano [[my_domain_name]].de.conf

        ...     Include /etc/apache2/imscp/[[my_domain_name]].de.conf
        >>>
        >>>     # 2018 11 22 peter: added redirect for ssl
        >>>     Redirect permament / https://[[my_domain_name]].de/
        >>>
        ... </VirtualHost>
~~~~~

## Additional Info
Editing imscp settings was always giving an error :-(

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
        >>> # 2018 11 22 peter: added redirect for ssl
        >>> Redirect / https://[[my_domain_name]].de/
        >>>
~~~~~


## other
[abbreviations](../log/abbreviations.md)
