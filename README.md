# Geo-Fence Jumping

This script will deploy a basic openvpn server instance and generate client
configuration files to connect to it. Because private keys are embedded into
the client configuration files to simplify client setup, this script should
not be used in security or privacy critical settings.

Usage:
This script must be run as root (run 'chmod +x ovpn_setup' to make it executable
if it isn't). It will attempt to determine the server's public IP to
use for the OpenVPN service, if multiple interfaces are found it will ask for
one to be specified. The -s and -e options only need to be run once to enable
the server, if multiple clients are desired the script should be run as many times
as necessary to generate unique client config files. If -d option is used and
the server FQDN resolves to the detected public IP, client config files will
use the FQDN instead of the IP.

Working on:
  Debian 7, 6
  Ubuntu 14.04, 12.04
  Centos 7, 6, 5
  Fedora 20, 19

Failing on:
  Ubuntu 15.10 (network init and firewall issues)

Known Issues:
  1) Does not handle unicode names, which would be hard.
  2) Will conflict with other uses of the 172.30.*.* subnet.
  3) Does not play nice with SELinux, and will disable it. To re-enable SELinux,
     run 'setenforce 1'. You will need to manually configure /etc/openvpn/ovpn_net.sh
     to run at boot (or find another way to make those settings persistent).

Needs testing:
  1) Client DNS updating, especially for linux clients.
  2) Routing of client DNS requests. Add a --route command to config?                