firewall-cmd --state
systemctl status firewalld
    masked and inactive
systemctl unmask firewalld
systemctl enable --now firewalld
firewall-cmd --list-all
    zone, target, icmp-block, interface, port, services, and more.
firewall-cmd --get-default-zone
firewall-cmd --list-services 
firewall-cmd --list-ports
firewall-cmd --remove-service={bitcoin,pop3,smtp,telnet,vnc-server,synergy,cockpit}
firewall-cmd --remove-port={101/tcp, 202/udp, 303/tcp,404/udp}
firewall-cmd --list-all
firewall-cmd --runtime-to-permanent 
firewall-cmd --reload
firewall-cmd --get-services
firewall-cmd --add-service={http,https} --permanent
firewall-cmd --reload
firewall-cmd --add-port=8080/tcp
firewall-cmd --reload
firewall-cmd --zone=block --add-source=10.0.0.13/24 --permanent
ssh -p 2222 client1
firewall-cmd --zone=drop --add-source=10.0.0.13/24 --permanent
firewall-cmd --zone=drop --remove-source=10.0.0.13/24 --permanent

firewall-cmd --get-default-zones 
firewall-cmd --get-zones

firewall-cmd --get-active-zones
    public 
        interfaces: enp1s0
firewall-cmd --change-interface=enp1s0 --zone=work --permanent
firewall-cmd --reload
firewall-cmd --set-default-zone=dmz
firewall-cmd --remove-interface=enp1s0 --zone=work --permanent 
nnmcli con mod "Wired connection 1" connection.zone public
firewall-cmd --get-zones
firewall-cmd --new-zone=custom --permanent
firewall-cmd --reload

firewall-cmd --list-all --zone=custom

firewall-cmd --permanent --zone=custom --add-source=10.0.0.13/24
firewall-cmd --list-all-zones
firewall-cmd --get-icmptypes | grep echo
firewall-cmd --add-icmp-block=echo-request --permanent
firewall-cmd --reload
firewall-cmd --list-all
firewall-cmd --remove-icmp-block=echo-request --permanent
firewall-cmd --add-icmp-block-inversion  #block all icmp 
