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
