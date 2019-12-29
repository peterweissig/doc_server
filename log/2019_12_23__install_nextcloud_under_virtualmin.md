# 2019 12 23 install nextcloud under virtualmin

[go back to nextcloud overview](../doc/nextcloud.md)


## Problem
After switching from imscp to virtualmin, all clouds were removed.
Therefore they need to be reinstalled.


## Solution
See also: https://nextcloud.com/install/#instructions-server

## Steps

### 1. create domain

Goto virtualmin gui and create new (sub)domain:

#### a) open virtualmin

~~~~~
    admin.[[my_domain_name]].de
    alternative: [[my_domain_name]].de:10000
~~~~~


#### b) create new (sub)domain

Goto settings:

~~~~~
    sidebar:
        [VirtualMin] --> [Create Virtual Server]
~~~~~

Fill out main window as desired.

Set:

~~~~~
    [x] Apache website enabled?
    [x] Apache SSL website enabled?
    [x] MySQL database enabled?
~~~~~

Unset:

~~~~~
    [ ] DAV login
    [ ] Webalizer reporting enabled?
    [ ] AWstats reporting
~~~~~

Finish:

~~~~~
    [Create Server]
~~~~~

#### c) add SSL-certificate

Goto settings:

~~~~~
    sidebar:
        [VirtualMin] --> [Server Configuration] --> [SSL Certificate]

~~~~~

Either \
add an existing certificate (upload it) \
or \
create a new one using letsencrypt!


#### d) add user

Goto settings:

~~~~~
    sidebar:
        [VirtualMin] --> [Edit Users]

    main window:
        [Add a user to this server]

~~~~~

Fill out main window as desired:

~~~~~
    Virtual domain user details
        Username : "mysql"   (mysql@[[subdomain]].[[domain]].de)
        Real name: ""        (can be left empty)
        Password : xxx       (don't change, but copy generated password!)
        ...
    ...
    Other user permissions
        ...
        Allow access to database:
            grant access to database "[[subdomain]](MySQL)"
~~~~~

Finish:

~~~~~
    [Create]
~~~~~

#### d) set php mode

Goto settings:

~~~~~
    sidebar:
        [VirtualMin] --> [Server Configuration] --> [Website Options]
~~~~~

Fill out main window as desired:

~~~~~
    Website and PHP Options
        ...
        PHP script execution mode: [x] FPM
    ...
~~~~~

Finish:

~~~~~
    [Save]
~~~~~

#### e) set php version

Goto settings:

~~~~~
    sidebar:
        [VirtualMin] --> [Server Configuration] --> [PHP Versions]
~~~~~

Fill out main window as desired!

Finish:

~~~~~
    [Save Versions]
~~~~~


### 2. install nextcloud


Check for current version.

~~~~~
     https://nextcloud.com/install/#instructions-server
~~~~~

#### a) download current version


~~~~~
    $ cd /home/[[domain]]/domains/[[subdomain]].[[domain]].de/public_html
    $ wget https://download.nextcloud.com/server/releases/nextcloud-17.0.1.zip

    $ unzip nextcloud-17.0.1.zip && rm nextcloud-17.0.1.zip
    $ chown -R [[username]]:[[username]] nextcloud
    $ mv nextcloud/* ./
    $ mv nextcloud/.htaccess ./
    $ mv nextcloud/.user.ini ./
    $ rmdir nextcloud/
~~~~~

#### b) open browser


~~~~~
    [[subdomain]].[[my_domain_name]].de/index.php/login
~~~~~

Fill out basic config:

~~~~~
    Administrator-Konto anlegen
        Benutzername: "admin"
        Passwort    : xxx (use a strong one)

    Speicher & Datenbank
        Datenverzeichnis:
          /home/[[domain]]/domains/[[subdomain]].[[domain]].de/public_html/data
        Datenbank einrichten:
            Datenbank-Benutzer: "mysql"
            Datenbank-Passwort: xxx (see 1.d))
            Datenbank-Name    : "[[subdomain]]"
            Datenbank-Host    : "localhost"
~~~~~

Finish:

~~~~~
    [Installation abschließen]
~~~~~



## other
[abbreviations](../log/abbreviations.md)
