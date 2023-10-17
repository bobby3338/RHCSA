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
     
     rm -fr /etc/yum.repos.d/*
    1. sudo vi /etc/yum.repos.d/local.repo              // sudo 
    2. name=baseOS
        baseurl=https://lab.example.com/baseOS
        gpgcheck=0
        enabled=1
        name=appStream
        baseurl=https://lab.example.com/appStream
        gpgcheck=0
        enabled=1
    Method 2: 
        rm -fr /etc/yum.repos.d/*  // delete all content in that directory
        vim /etc/yum.repos.d/yum.repo
        [exam]
        name=exam
        baseurl=http://content.example.com/rhel7.0/x86_64/dvd
        gpgcheck=0
        enable=1
        
Task 3:  Tuned profile in Linux 
    1. dnf install tuned
    2. systemctl enable tuned
    3. systemctl start tuned
    4. tuned-adm list                       //view options
    5. tuned-adm profile virtual-guest 
    6. important commands   
        tuned-adm recommend/active/profile/off/list

Task 4:  




Task 11.  Partition and Swap management
Part 1: Partion and mount
    1. lsblk
    2. ls /dev
    3. fdisk /dev/nvme0n2
    4. m - help, n - new
    5. +1GB
    6. default type is linux, there are options to change such as swap
    7. w - write the partition table
    8. partprobe /dev/nvme0n2               // if you don't see the partition
    9. mkdir /newdisk 
    10. mkfs.xfs /dev/nvme0n2p1 
    11. mount /dev/nvme0n2p1 /newdisk
    12. vi /etc/fstab
        /dev/nvme0n2p1  /newdisk    xfs     default 0   0
    13. mount -able
    14. lsblk

Part 2: Method 1:
    1. free -m 
        Swap:           2047           0        2047
    2. fdisk /dev/nvme0n2
    3. n, 3, +750MB,
    4. t - change type 
    5. L to view Hex code 
    6. 82 swap
    7. w - write
    8. mkswap /dev/nvme0n2p3
    9. vi /etc/fstab 
        /dev/nvme0n2p3 swap swap default 0 0 
    10. swapon -a / swapon /dev/nvme0n2p3
    11. swapoff /dev/nvme0n2p3

        Method 2:
    1. dd if=/dev/zero of=/swapfile bs=1M count=750
        dd - create swap file, if=/dev/zero input file or storage, of=/swapfile output file name /swapfile, bs=1M block size of 1MB, count=750 create 750 block of 1MB 
        750+0 records in
        750+0 records out
        786432000 bytes (786 MB, 750 MiB) copied, 2.53381 s, 310 MB/s
    2. du -sh /swapfile
        du disk use, -s specify directory -h human readable
        750M	/swapfile
    3. mkswap /swapfile 
        mkswap: /swapfile: insecure permissions 0644, fix with: chmod 0600 /swapfile
        Setting up swapspace version 1, size = 750 MiB (786427904 bytes)
        no label, UUID=c0c95676-8ebe-42ce-848b-18eb3ba9bd51
        -rw-r--r--. 1 root root 786432000 Oct 11 12:15 /swapfile
    4. chmod 0600 /swapfile
        -rw-------. 1 root root 786432000 Oct 11 12:15 /swapfile
    5. vi /etc/fstab 
        /swapfile swap swap defaults 0 0 
    6. swapon -a 


