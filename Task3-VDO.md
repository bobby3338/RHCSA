Creating virtual data optimizer 
    1. yum info lvm*                        //
    2. dnf install lvm*
    3. lsblk 
    4. pvcreate /dev/nvme0n2                //physical volume 
        pvs                                     //view physical volume
    5. vgcreate VG1 /dev/nvme0n2            //volume group
        vgs                                     //view volume group
    6. lvcreate --type vdo --name VDO1 --size 5GB --virtualsize 50GB VG1  // size 5GB to Virtualsize 50GB 1:10 
    7. mkfs.xfs -K /dev/VG1/VDO1            //format the filesystem to xfs -K filesystem created with no    discard option.
    8. mkdir /mnt/vdo
    9. lvdisplay
    10. cat /etc/fstab
    11. vi /etc/fstab                       //add the VDO to the booting 
        /dev/VG1/VDO1       /mnt/vdo                  xfs      default          0              0 
        VDO1 absolute path  Mounting Directory    filesystem default mount  dump back up   filesystem check 
    13. mount -a 
    14. lsblk 
2. Create LVM 
3. 
4. 
5.
