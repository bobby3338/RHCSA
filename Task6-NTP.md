Task: 
    Setting NTP server
        dnf install chronyc
        vi /etc/chrony.conf
        comment out the pool 2.rhel.pool.ntp.org iburst
        add server classroom.example.com / <ip addr> iburst
        systemctl restart chronyd
        systemctl enable chronyd
        chronyc sources -c 
        timedatectl                          //check status
        timedatectl set-ntp true
        systemctl status chronyd