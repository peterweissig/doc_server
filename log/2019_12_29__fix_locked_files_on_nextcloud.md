# 2019 12 29 fix locked files on nextcloud

[go back to nextcloud overview](../doc/nextcloud.md)


## Problem
Sometimes files stay locked after they were removed or
after connection problems from clients.


## Solution
Check for updated files on server and eventually remove file locks manually.


## Steps

### 1. recheck for files

File checking may take a while. Maybe work within a screen-session.


~~~~~
    $ cd /home/[[domain]]/domains/[[subdomain]].[[domain]].de/public_html

    $ sudo -u [[username]] php occ files:scan --all
~~~~~

#### 2) remove file locks

If files are still locked - remove file locks manually!

~~~~~
    $ cd /home/[[domain]]/domains/[[subdomain]].[[domain]].de/public_html

    $ sudo -u [[username]] php occ files:scan --all
~~~~~

Fill out basic config:

~~~~~
    $ mysql
        > use [[subdomain]];
        > SELECT * from oc_file_locks WHERE 1;
~~~~~

Are there the problematic entries ?

~~~~~
        > DELETE FROM oc_file_locks WHERE 1;
~~~~~

Finish:

~~~~~
    <strg>+<d>
~~~~~



## other
[abbreviations](../log/abbreviations.md)
