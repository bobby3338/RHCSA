Creating partition and make file system to mount
    fdisk /dev/nvme0n2
    cfdisk /dev/nvme0n2
    fdisk -l /dev/vd{b,c}
    l to view partition type
    t to change partition time
    mkfs.vfat -f 32 /dev/vdb1
        -f format size, default if empty
    fatlabel /dev/vdb1 Myfat
    mkfs.ext4 -E nodiscard /dev/vdb2
        -E no discard
    e2label /dev/vdb2 Myext4
    mkfs.xfs -f -K /dev/vdb3
        -f force, if data exists, -K no discard  
    xfs_admin -L Myxfs /dev/vdb3
        -L label   
    blkid 
    
    mkdir /mnt/{myfat,myext4,Myxfs}
    vim /etc/fstab
        LABEL=Myfat     /mnt/myfat  vfat    defaults 0  0
        UUID=           /mnt/Myext4     acl    defaults 0 0 
        /dev/vdb3       /mnt/Myxfs      xfs     defaults 0 0 
    df 
    mount -a 
   
Creating virtual data optimizer 
    1. yum info lvm* // 
    2. dnf install lvm* 
    3. lsblk 
    4. pvcreate /dev/nvme0n2 //physical volume
                pvs //view physical volume 
    5. vgcreate VG1 /dev/nvme0n2 //volume group
                vgs //view volume group 
    6. lvcreate --type vdo --name VDO1 --size 5GB --virtualsize 50GB VG1 // size 5GB to Virtualsize 50GB 1:10 
    7. mkfs.xfs -K /dev/VG1/VDO1 //format the filesystem to xfs -K filesystem created with no discard option. 
    8. mkdir /mnt/vdo 
    9. lvdisplay 
    10. cat /etc/fstab 
    11. vi /etc/fstab //add the VDO to the booting
        /dev/VG1/VDO1 /mnt/vdo xfs default 0 0
        VDO1 absolute path Mounting Directory filesystem default mount dump back up filesystem check 
    12. mount -a 
    14. lsblk
Swap management
    Part 1: Partion and mount 
    1. lsblk 
    2. ls /dev 
    3. fdisk /dev/nvme0n2 
    4. m - help, n - new 
    5. +1GB 
    6. default type is linux, there are options to change such as swap 
    7. w - write the partition table 
    8. partprobe /dev/nvme0n2 // if you don't see the partition 
    9. mkdir /newdisk 
    10. mkfs.xfs /dev/nvme0n2p1 
    11. mount /dev/nvme0n2p1 /newdisk 
    12. vi /etc/fstab
        /dev/nvme0n2p1 /newdisk xfs default 0 0 
    13. mount -able 14. lsblk

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
