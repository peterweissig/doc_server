# 2019 01 04 upgrade imscp

[go back to imscp overview](../doc/imscp.md#update-imscp)


## Problem
imscp needs an update \
(info via web-gui and via mail)


## Solution
Follow explanation step-by-step.

See also https://github.com/i-MSCP/imscp/blob/1.5.x/docs/Debian/INSTALL.md \
And check website for current versions: https://i-mscp.net/

## Steps

### 1. check errata
e.g. https://github.com/i-MSCP/imscp/blob/1.5.3/docs/1.5.x_errata.md

### 2. create backups
See [2019 01 04 backup data](../log/2019_01_04_001__backup_data.md)

### 3. update server

~~~~~
    $ apt-get update
    $ apt-get --assume-yes --auto-remove --no-install-recommends dist-upgrade
~~~~~

### 4. download files

~~~~~
    $ mkdir -p ~/install/imscp/ && cd ~/install/imscp/
    # check websites for current versions
        # https://i-mscp.net/
        # https://github.com/i-MSCP/imscp
        # As for now the current verion is 1.5.3
    $ wget https://api.github.com/repos/i-MSCP/imscp/zipball/1.5.3-2018120800
    $ unzip 1.5.3-2018120800 && rm 1.5.3-2018120800
    $ mv i* 1.5.3-20181208 && cd 1.5.3-20181208
~~~~~


### 5. (re-)install imscp

~~~~~
    $ perl imscp-autoinstall -d
~~~~~
