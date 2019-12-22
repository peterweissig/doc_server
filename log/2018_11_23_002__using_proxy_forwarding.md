# 2018 11 23 using proxy forwarding

[go back to imscp overview](../doc/imscp.md#forwarding)


## Problem
Using standard redirection (e.g. 301, 302, ...) will display the url
of destination site. \
E.g. mail.[[my_domain_name]].de ==301==> [[server_url]]:8433/mail

This looks ugly and should be displayed as mail.[[my_domain_name]].de, while
internally accessing [[server_url]].


## Solution
Change settings in imscp-panel for domain.


## Steps

### 1. login into imscp panal (as customer)

### 2. go to "domains"

### 3. add subdomain or change settings of subdomain

~~~~~
    URL forwarding    Yes
    Forward to URL    https://   <server-url>
    Forward type      PROXY
~~~~~


## other
[abbreviations](../log/abbreviations.md)
