Problem:
    Imscp backs up mail, databases and web automaticaly (daily).
    Email and databases are (for now) small enough.
    But webspace backup is to big!.

Sidenote:
    See also file "2019_01_04_001__backup_data.txt")

Solution:
    Turn setting off in webinterface.

###########################################################################

0. check size of backups
    $ ll -h /var/www/virtual/*/backups/

1. log into imscp-gui as reseller
  a) go to "customers"
  b) search for customer/domain
  c) click on "edit domain" ("Domain bearbeiten")
      # scroll down to properties ("Merkmale")
      # search for Backup
      # deactivate "Domain"

3. done :-)
