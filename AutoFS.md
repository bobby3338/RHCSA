1. Creating AutoFS
    1. dnf install nfs*
    2. mkdir /shared
    3. touch /shared/t1 /shared/t2 /shared/t3
    4. ls -l /shared
        -rw-r--r--. 1 root root 0 Oct 10 12:27 t1
        -rw-r--r--. 1 root root 0 Oct 10 12:27 t2
        -rw-r--r--. 1 root root 0 Oct 10 12:27 t3
    5. chmod 777 /shared
    6. vi /etc/exports
        /shared             192.168.43.22(ro, sync)     // ip addr of client
        folder to shared    remote host ip addr     ro / read only rw / read write     sync / syncrhonous mode?
    7. exportfs -avr                        //NFS exports, -a all directories listed, -r refresh, -v verbose.
            exporting 192.168.43.22:/shared             //client ip
    8. firewall-cmd --add-service={nfs.mountd.rpc-bind} --permanent  // didn't work ?
    9. firewall-cmd --add-service=nfs --add-service=mountd --add-service=rpc-bind --permanent
    10. firewall-cmd --reload
      
        Client 
    1. showmount -e 192.168.43.237          //-e display the list of exports on the specified NFS server
    2. vi /etc/auto.master
    3. #/misc   /etc/auto.misc              //comment out
    4. /auto_mount /etc//auto.misc --timeout=30     //timeout optional
        remote      local 
    5. vi /etc/auto.misc                    //
    6. access       -rw,soft,intr       192.168.43.237:/shared
    7. systemctl enable autofs --now
    8. ls /
    9. cd auto_mount
    10. ls
    11. cd access
    12. ls
    13. t1, t2,t3