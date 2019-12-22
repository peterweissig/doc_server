# 2019 08 31 disable login via password

[go back to server overview](../doc/server.md#login)


## Problem
External users (bots) try to login and bruteforce the password.


## Solution
Disable login by password.

See also: https://security.stackexchange.com/questions/21027/
  (invalid-users-trying-to-log-in-to-my-server)


## Steps

### 1. check current entries

~~~~~
    $ journalctl -xe
    $ tail /var/log/auth.log
~~~~~

### 2. disable password

~~~~~
    $ sudo nano /etc/ssh/sshd_config
        ... # To disable tunneled clear text passwords, change to no here!
        ... #PasswordAuthentication yes
        >>> # 2019 08 31 peter: turned off login by password
        >>> PasswordAuthentication no
        ... #PermitEmptyPasswords no

~~~~~

### 3. restart deamon

~~~~~
    $ service ssh restart

    # old behaviour (bad)
    #    $ sudo systemctl status sshd.service
~~~~~
