Task 1: Configure TCP/IP and "hostname" as following:
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
    6. hostnamectl set-hostname serverX.example.com
    7. route -n                         //to show gateway
    8. Cat /etc/resolv.conf

Task 2: Configuring repositories in Linux
    Example of repo
        name = Red Hat OpenShift Container Platform 4.13 for RHEL 9 x86_64 (RPMs)
        baseurl = https://cdn.redhat.com/content/dist/layered/rhel9/x86_64/rhocp/4.13/os
        enabled = 0
        gpgcheck = 1
     
    1. sudo vi /etc/yum.repos.d/local.repo              // sudo 
    2. name=baseOS
        baseurl=https://lab.example.com/baseOS
        gpgcheck=0
        enabled=1
        name=appStream
        baseurl=https://lab.example.com/appStream
        gpgcheck=0
        enabled=1

Task 3:  Tuned profile in Linux 
    1. dnf install tuned
    2. systemctl enable tuned
    3. systemctl start tuned
    4. tuned-adm list                       //view options
    5. tuned-adm profile virtual-guest 
    6. important commands   
        tuned-adm recommend/active/profile/off/list

Task 4:  Setting NTP server
    1. dnf install chronyc
    2. vi /etc/chrony.conf
    3. comment out the pool 2.rhel.pool.ntp.org iburst
    4. add server <ip addr> iburst
    5. systemctl restart chronyd
    6. chronyc sources -c 
    7. timedatectl                          //check status
    8. timedatectl set-ntp true
        systemctl status chronyd

Task 5:  Create users and groups
    1. groupadd group1
    2. useradd user1 -G group1              //-G specify the intial login group for the user1
    3. useradd user2 -s /sbin/nologin       //-s specify login shell sbin/nologin indicate no interactive logins.
    

