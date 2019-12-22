# 2019 08 31 try autoupdate imscp-certificate

[go back to imscp overview](../doc/imscp.md#certificates)


## Problem
Websites (e.g. imscp) and clouds do not work.

imscp(via internal redirect) and clouds: empty webpage \
imscp(direct): ssl-error


## Solution
Automatically update letsencrypt-certificate for imscp main page.


## Steps

### 1. create cron-job

~~~~~
    $ sudo nano /etc/cron.daily/copy_letsencrypt_certificates_to_imscp
        # for content see next section

    $ sudo chmod a+x /etc/cron.daily/copy_letsencrypt_certificates_to_imscp
~~~~~

## File content

~~~~~
    #!/bin/sh

    # /etc/cron.daily/copy_letsencrypt_certificates_to_imscp

    # setup parameters
    CERT_NAME="[[server_url]]"
    MAIL_TARGET="[[mail]]"

    # init variables
    cert_path="/etc/letsencrypt/live/${CERT_NAME}/"
    dest_file="/etc/imscp/${CERT_NAME}.pem"
    temp_file="${dest_file}.temp"

    # check if files exist
    if [ ! -d "$cert_path" ] || [ ! -f "$dest_file" ]; then
        (
            echo "$0"
            echo "  # script for updating imscp-certificate"
            [ -d "$cert_path" ] || \
                echo "  directory \"$cert_path\" does not exist."
            [ -f "$dest_file" ] || \
                echo "  file \"$dest_file\" does not exist."
        ) | mail -s "IMSCP-Server: Error during certificate check" \
            "$MAIL_TARGET"
        exit 0
    fi

    # create temp-certificate
    (
        cat "${cert_path}privkey.pem"
        cat "${cert_path}cert.pem"
        cat "${cert_path}chain.pem"
    ) > "${temp_file}"

    # compare certificates
    [ -z "$(diff -q "${temp_file}" "${dest_file}")" ] && exit 0

    # send email
    (
        echo "$0"
        echo "  # script for updating imscp-certificate"
        echo "  certificate for \"$CERT_NAME\" was updated"
        echo "  file will be updated."
    ) | mail -s "IMSCP-Server: Updating certificate" \
        "$MAIL_TARGET"

    # update certificate
    # cp "${temp_file}" "${dest_file}"
~~~~~


## other
[abbreviations](../log/abbreviations.md)
