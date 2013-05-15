Support Keys
============

This repository contains all of the ssh public keys needed to allow Acquia Support access to remote servers.

Files
-----

### ip_whitelist
This file contains all of the Acquia IPs that will be used to access remote systems.

### authorized_keys
This file contains all of the ssh public keys that Acquia Support will use to access remote systems. This format also enforces access through Acquia's networks via Ip whitelisting using the IPs in the ip_whitelist file.

### authorized_keys_no_whitelist
This file contains all of the ssh public keys that Acquia Support will use to access remote systems. This format omits and ip whitelisting and should be used when there is a VPN required to access the remote systems.

Installation Instructions
-----
#### Please create and provide the user acquia_support with the following permissions:
  * R+W+X for all site docroot files within dev, staging and production.
  * R+W+X for all VCS folders and files.
  * X for drush folder, RW if you would like acquia_support to be able to update drush itself.
  * R+W+X for mysql databases, ability to run mysql.
  * R for all log files.

#### To initially setup the ssh folder for the acquia_support user, run this command: 

mkdir -pm 700 ~/.ssh > /dev/null 2>&1 ; curl --silent --write-out \%{http_code} https://raw.github.com/acquia/support_keys/master/authorized_keys --output ~/.ssh/authorized_keys_dl 2> /dev/null | grep 200 > /dev/null && mv -f ~/.ssh/authorized_keys_dl ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys > /dev/null 2>&1

#### Update the ssh folder via crontab:
Run 'crontab -e' and add this line:

0 0 * * * mkdir -pm 700 ~/.ssh > /dev/null 2>&1 ; curl --silent --write-out \%{http_code} https://raw.github.com/acquia/support_keys/master/authorized_keys --output ~/.ssh/authorized_keys_dl 2> /dev/null | grep 200 > /dev/null && mv -f ~/.ssh/authorized_keys_dl ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys > /dev/null 2>&1

This crontab runs every day at midnight (you may change the time), creating and updating a folder which contains the authorized public key files of Acquia Client Advisors.

VPN and Keys:
-----
It is our strong recommendation that rather than depend on VPN or passwords, we use authorized key files and whitelisting. If VPN is required, you must also use this alternative crontab entry which removes the ip whitelisting as this will not work from within the VPN subnet:

0 0 * * * mkdir -pm 700 ~/.ssh > /dev/null 2>&1 ; curl --silent --write-out \%{http_code} https://raw.github.com/acquia/support_keys/master/authorized_keys_no_whitelist --output ~/.ssh/authorized_keys_dl 2> /dev/null | grep 200 > /dev/null && mv -f ~/.ssh/authorized_keys_dl ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys > /dev/null 2>&1
