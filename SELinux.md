set SELinux mode
    1. getenforce
    2. setenforce 0                     // 0 permissive 1 enforcing 
    3. vi /etc/sysconfig/selinx         //
    4. SELINUX=disabled                 //reboot

        set boolean value
    1. getsebool -a                        //see all option
    2. getsebool -a | grep "httpd"
    3. setsebool -P httpd_enable_homedirs on  //reboot required
        -P persistent on reboot
        SELinux port
    1. semanage port -a -t http_port_t -p tcp 82
        semanage port -add -type http_port_t -protocol tcp 82 port
    
        httpd service is able to access and host files from the /test directory
    1. ls -l /var/www/html
    2. touch /var/www/html/index.html  
        Learning Linux index.html
    3. mkdir /test
    4. touch /test/index.html
    5. vi /test/index.html
    6. ls -lZ /var/www/index.html                   // Z display SELinux security contect 
        -rw-r--r--. 1 root root unconfined_u:object_r:httpd_sys_content_t:s0 26 Oct 11 10:26 index.html
    7. ls -lZ /test
        -rw-r--r--. 1 root root unconfined_u:object_r:default_t:s0 16 Oct 11 10:29 index.html
    8. semanage fcontext -a -t httpd_sys_content_t "/test(.*)?"       //set the file context  
        semanage file context -a add, - t type httpd_sys_content_t (security context for web server files), "/test(.*)?" any files or directory matches any characters.
    9. restorecon -Rv /test                        // relabel the file context
    10. ls -lZ /test
        -rw-r--r--. 1 root root unconfined_u:object_r:httpd_sys_content_t:s0 16 Oct 11 10:29 index.html
        file content type changed to httpd_sys_content_t
    11. vi /etc/httpd/conf/httpd.conf              // changing the default "DocumentRoot="/var/www/html" "Directory "/var/www/"
        DocumentRoot="/test"  Directory "/test"
    12. systemctl restart httpd
    13. curl localhost