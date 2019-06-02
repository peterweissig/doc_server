Problem:
    New nextcloud version is available. But updater is frozen at step 3.

Solution:
    Using console to do update.
    See also:
      docs.nextcloud.com/server/15/admin_manual/maintenance/update.html

###########################################################################

1. got to installed nextcloud directory
    $ cd /var/www/virtual/<my_domain_name>.de/<subdomain>/htdocs/

2. check for running updates
    $ find -name .step
    # e.g. data/updater-ocj8604f9zjm/.step

    # cat data/updater-*/.step
    # rm data/updater-*/.step

3. goto updater folder
    $ cd updater

4. check for html-user name
    $ ls -la

5. execute update
    $ sudo -u <username> php updater.phar

        ...
        "Start update? [y/N]"
            <y>
            <enter>

        ...
        "Update of Code successful."
        "Should the occ upgrade command be executed? [Y/n]"
            <enter>

        ...
        "Keep maintenance mode active? [y/N]"
            <enter>

(6. additional conversion steps)
  see also docs.nextcloud.com/server/15/admin_manual/maintenance/upgrade.html
  #upgrading-to-nextcloud-13
    $ cd ..
    $ sudo -u <username> php occ db:add-missing-indice
    $ sudo -u <username> php occ db:convert-filecache-bigint
        ...
        "Continue with the conversion (y/n)? [n]"
            <y>
            <enter>

done :-)
