Creating NFS
    Server 
    1. yum install nfs
    2. mkdir -p /mnt/nfs
    2. groupadd -g 12345 fun
    3. usermod -aG fun admin
    4. chown :fun /mnt/nfs
    5. chmod g+s /mnt/nfs
    6. chmod g+w /mnt/nfs
    6. vi /etc/export
        /mnt/nfs    192.168.0.1/24(sync, rw)
    7. firewall-cmd --permanent --add-service nfs
    8. systemctl enable nfs-server
    
    Client
    1. mkdir -p /mnt/nfs
    2. yum install nfs-utils
    3. groupadd -g 12345 fun
    4. usermod -aG fun admin
    5. mount -t nfs server:/mnt/nfs /mnt/nfs
    6. umount /mnt/nfs
    7. vi /etc/fstab
    8. server:/mnt/nfs /mnt/nfs nfs defaults 0 0 
    9. mount -a 
    10. df 

Creating AutoFS
    Server 
    1. dnf install nfs*
    2. mkdir /mnt/server/autofs 
    3. touch /mnt/server/autofs/t1, t2, t3,
    4. ls -l /mnt/autofs 
        -rw-r--r--. 1 root root 0 Oct 10 12:27 t1
        -rw-r--r--. 1 root root 0 Oct 10 12:27 t2
        -rw-r--r--. 1 root root 0 Oct 10 12:27 t3
    5. chmod 777 /mnt/server/autofs 
    6. vi /etc/exports   
        /mnt/server/autofs             192.168.43.22(ro, sync)     // ip addr of client
        folder to shared    remote host ip addr     ro / read only rw / read write     sync / syncrhonous mode?
    7. exportfs -avr                        
            -a all directories listed, -r refresh, -v verbose.
            exporting 192.168.43.22:/mnt/autofs            //client ip
    8. firewall-cmd --add-service={nfs.mountd.rpc-bind} --permanent  
    9. firewall-cmd --add-service=nfs --add-service=mountd --add-service=rpc-bind --permanent
    10. firewall-cmd --reload
      
        Client 
    1. showmount -e 192.168.43.237          //-e display the list of exports on the specified NFS server
    2. mkdir /mnt/autofs 
    2. vi /etc/auto.master
    3. #/misc   /etc/auto.misc              //comment out
    4. /mnt/server/autofs /etc//auto.direct --timeout=30     //timeout optional
        remote      local 
    5. vi /etc/auto.direct                    //
        /mnt/autofs     -rw,soft,intr       192.168.43.237:/mnt/server/autofs 
    6. systemctl enable autofs --now
    7. df 
    8. ls
    9. t1, t2,t3

        Indirect
    vi /etc/auto.master 
    /mnt/nfs    /etc/auto.indirect 
    vi /etc/auto.indirect
        * server:/mnt/autofs 
    systemctl restart autofs
    df 