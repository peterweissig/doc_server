# 2019 01 04 restrict backups

[go back to imscp overview](../doc/imscp.md#backup)


## Problem
Imscp backs up mail, databases and web automaticaly (daily). \
Email and databases are (for now) small enough. \
But webspace backup is to big!

Sidenote:
* See also [2019 01 04 backup data](../log/2019_01_04_001__backup_data.md)


## Solution
Turn setting off in webinterface.


## Steps
### 1. check size of backups

~~~~~
    $ ll -h /var/www/virtual/*/backups/
~~~~~

### 2. log into imscp-gui as reseller
#### a) go to "customers"
#### b) search for customer/domain
#### c) click on "edit domain" ("Domain bearbeiten")

scroll down to properties ("Merkmale")

search for Backup

deactivate "Domain"
