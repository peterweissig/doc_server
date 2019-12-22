# 2018 11 21 install certbot

[go back to server overview](../doc/server.md#letsencrypt)

## Info
* https://letsencrypt.org/
* https://certbot.eff.org/lets-encrypt/debianstretch-other
* https://backports.debian.org/Instructions/

## Steps

1. update sources list
    ```
    $ cd /etc/apt/
    $ nano sources.list
        ... deb http://mirror.ip-projects.de/debian stretch main non-free contrib
        ... deb-src http://mirror.ip-projects.de/debian stretch main non-free contrib
        ... deb http://mirror.ip-projects.de/debian stretch-updates main non-free contrib
        ... deb-src http://mirror.ip-projects.de/debian stretch-updates main non-free contrib
        ... deb http://mirror.ip-projects.de/debian-security stretch/updates main non-free contrib
        ... deb-src http://mirror.ip-projects.de/debian-security stretch/updates main non-free contrib
        >>>
        >>> # 2018 11 22 peter: for letsencrypt
        >>> deb http://mirror.ip-projects.de/debian stretch-backports main
        ...
        ... ## Dotdeb Packages
        ... ##deb http://packages.dotdeb.org stretch all
        ... ##deb-src http://packages.dotdeb.org stretch all
        ...
        ... deb https://packages.sury.org/php/ stretch main
        ... deb-src https://packages.sury.org/php/ stretch main
    ```

2. update apt

    ```
    $ apt-get update
    $ apt-get upgrade
    ```

3. install certbot

    ```
    $ apt-get install certbot -t stretch-backports
    ```
