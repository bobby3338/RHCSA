ssh root@server

ssh -p 2222 root@server
    -p specify the port
ls -la 
    .ssh directory created permission 700 by default
vim .ssh/config  
    creating alias 
        Host client1
        Hostname client1
        User    root
        Port    2222
        IdentityFile ~/.ssh/coolkey

    chmod 600 .ssh/config

ssh-keygen 
    generating id_rsa and id-rsa.pub  

ssh-keygen -t rsa -b 4096 -N "" -f .ssh/coolkey
    -t type -b size     -N paraphrase -f specify file output
ssh-copy-id client1 
    copy key to client1 

ssh-copy-id -i .ssh/coolkey client1
    -i identityfile
ssh -o StrictHostKeyChecking=no client1
vi .ssh/known_hosts 
    remove the old key
vi /etc/ssh/sshd_config
    PermitRootLogin yes
    change port / x11 forwarding
Port 2222
    dnf policycoreutils-python-utils must be installed for semanage
    semanage port -a -t ssh_port_t -p tcp 2222
    firewall-cmd --add-port 2222/tcp --permanent
    firewall-cmd --reload
    systemctl restart sshd


