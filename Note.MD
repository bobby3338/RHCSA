Note from 09/17/23
    BIOS: /boot/grub2/grub.cfg
    UEFI: /boot/efi/EFI/redhat/grub.efi
    daemon = system service
        systemd service replaced system V init
        systemctl list-unit-files -at service  //show all enabled (-a)(-t) service file
        systemctl list-units -at service   //show all serivce in 5 column   
        syste2023-10-23-06-51-45.png2023-10-23-06-51-45.pngmctl list units -t service --state running  //filter running service
        systemctl status rsyslog  // show status of rsyslog
        sudo systemctl stop atd // to stop a service -- atd
        sudo systemctl start atd // to start
        systemctl restart atd // to restart
        systemctl is-active atd // to check if system is active
        systemctl mask atd // to prevent atd from starting, it is still active if it is started.  unmask to reverse.
        systemctl disable atd // to disable  // to check -- is-enabled // to enable --enable
    
        hostnamectl  
    Network interface Naming
        Firmware = eno1
        PCI Express slot = ens1
        PCI slot = enp1s0
        Invalid Firmware information = eth0
    // to configure network
        ip
        nmcli
        Nmtui
        nm-connection-editor

    // back to home directory
        cd ~  (root/home)
    //
        timedatectl set-timezone
        timedatectl set-time "2020-08-15 2300"
        timedatectl set-ntp true
//creating at job
    at now + 5min
    mkdir ~/Documents.bak 
    rsync -a ~/Documents/ ~/Documents.bak
    atq ( at job queue, will show a job number)
    at -c 4 
    atrm 4 ( to remove at job)
    at (runs job at specific time) batch job ( only the load is below 0,8)
    batch (batch job)
    touch
    ls -l ~/batchfile.txt

// Cron job 
    /Minute /Hour /Day /Month /Date of Week /Command to Run



