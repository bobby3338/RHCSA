1. Create User and group
       1. groupadd group1
    2. useradd user1 -G group1              //-G specify the intial login group for the user1
    3. useradd user2 -s /sbin/nologin       //-s specify login shell sbin/nologin indicate no interactive logins.
    4. cat /etc/passwd                      //user2:x:1002:1003::/home/user2:/sbin/nologin
    5. passwd user2                         //password change
        user1:!!:19640:0:99999:7:::         //!! indicate no password set for user1
        user2:$6$eQZa4mul1Pbj8A89$N.9XRpbDtaGh9Tv8pcq6dieU6fHWSaM3wIZsfJj13VTCnYAxOHaseJq7DW.hs8hhp9plDoiyz2w3nVN.Kqt5E0:19640:0:99999:7:::
    6. cp /etc/fstab /var/fstab             //copy from directory to directory
    7. ls -l /var/fstab                     //-rw-r--r--. 1 root root 579 Oct 10 10:23 /var/fstab 
    7. chown user1 /var/fstab               //change owner  -rw-r--r--. 1 user1 root 579 Oct 10 10:23 /var/fstab
    8. useradd user3                        //add user3
    9. setfacl -m u:user3:rw /var/fstab     //setfacl - set ACL to user3 
        //-m modify user:user3:read&write directory
    10. getfacl /var/fstab                  
        # file: var/fstab
        # owner: root
        # group: root
        user::rw-
        user:user3:rw-
        group::r--
        mask::rw-
        other::r--
    11. groupadd Mac
    12. setfacl -m g:Mac:--- /var/fstab
        //-m modify group:Mac:---  rwx directory ACL apply to.
        # file: var/fstab
        # owner: root
        # group: root
        user::rw-
        user:user3:rw-
        group::r--
        group:Mac:---
        mask::rw-
        other::r--
    13. mkdir /Linux
    14. chown :Mac /linux                   //: indicate changing the group ownership
    15. ls -ld /linux                       //d - directory
        //drwxr-xr-x. 2 root Mac 6 Oct 10 10:49 /linux
    16. touch /linux/ti
    17. ls -l /linux                        //- - file
        //-rw-r--r--. 1 root root 0 Oct 10 10:56 t1  
    18. chown -R :Mac /linux                //-R - Recursive, apply to content of the directory
        //-rw-r--r--. 1 root Mac 0 Oct 10 10:56 t1
    19. chmod g+s /linux                    //set GID group +s stickybit - default for future directories and files. 
    20. touch /linux/t2
    21. mkdir /linux/t3
    22. ls -l /linux
        -rw-r--r--. 1 root Mac  0 Oct 10 10:56 t1
        -rw-r--r--. 1 root Mac  0 Oct 10 11:05 t2
        drwxr-xr-x. 2 root Mac  0 Oct 10 11:08 t3
    23. getfacl /linux
        # file: linux
        # owner: root
        # group: Mac
        # flags: -s-
        user::rwx
        group::r-x
        other::r-x

    23. chmod +t /linux                     //set the sticky bit on the directory enforcing ownership-based deletion and renaming
        # file: linux
        # owner: root
        # group: Mac
        # flags: -st
        user::rwx
        group::r-x
        other::r-x
    24. ls -ld /linux 
        drwxr-sr-t. 3 root Mac 36 Oct 10 11:11 /linux

创建一个共享目录
    a) 创建一个共享目录/home/managers 特性如下
    b) /home/managers 目录的所有权时 sysmgrs
    c) Sysmgrs 组成员对目录有读写和执行的权限。初此之外的其他所有用户没有任
        何权限(root 用户除外)
    d) 在/home/managers 目录中创建的文件,其组所有权会自动设置为属于 sysmgrs组
        mkdir -p /home/managers
        chgrp sysmgrs /home/managers
        chmod 2775 /home/managers

3. Add user with user id and password
    useradd -u 1055 redhat 
    echo redhat | passwd --stdin redhat
    


