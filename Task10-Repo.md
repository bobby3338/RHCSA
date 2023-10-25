Creating Local repository
    1. mkdir 
    


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
        