Question 1:
Configure TCP/IP and "hostname" as following:
IP ADDRESS = 172.25.X.11
NETMASK = 255.255.255.0
GATEWAY = 172.25.X.254
DNS = 172.25.254.254
Hostname = serverX.example.com

1. Login as root
2. Nmtui
3. Edit a connection.
4. IPV4 set to manual.
5. Set the ip address, netmask, gateway, and dns. (DNS and Gateway should be the same.)
6. route -n to show gateway
7. Cat /etc/resolv.conf

SSH?

1. SSH root@servera

