Task 9: Managing Container podman
    Part 1:
    1. dnf install podman*
    2. podman login                 //use redhat login
    3. podman search httpd          // view the container link address
    4. podman pull docker.io/library/httpd
    5. podman images                //view the containers
        REPOSITORY               TAG         IMAGE ID      CREATED      SIZE
        docker.io/library/httpd  latest      359570977af2  3 weeks ago  173 MB
    6. podman rmi httpd            //rmi remove image ( this is an example of rmi )
    7. podman run -d --name web1 359570977af2   // run the container 
        command -d detached mode run in the background, --name for the container, id of the container.
    8. podman ps                    // view podman running service 
        6a4e5a3d030e  docker.io/library/httpd:latest  httpd-foreground  2 minutes ago  Up 2 minutes              web1
    9. podman run -d --name web2 -p 8080:80 359570977af2  // run web2 with specific port 
    10. podman ps
        TATUS        PORTS                 NAMES
        6a4e5a3d030e  docker.io/library/httpd:latest  httpd-foreground  4 minutes ago  Up 4 minutes                        web1
        ec7ca7be74bb  docker.io/library/httpd:latest  httpd-foreground  8 seconds ago  Up 9 seconds  0.0.0.0:8080->80/tcp  web2
    11. podman stop web1            //stopping web1 service
    12. podman rm web1              // remove web1
    13. podman run -it 359570977af2 /bin/bash 
        -it interactively, container id, using /bin/bash.
        root@49990c591579:/usr/local/apache2#           // apache commandline
    14. find / -name index.html                // search inside apache server
        /usr/local/apache2/htdocs/index.html
    15. exit to root@localhost
    16. mkdir /web                  //make a directory for mounting
    17. touch /web/mypage.html      //make an html page
    18. podman run -d --name web5 -p 8081:80 -v /web:/usr/local/apache2/htdocs 359570977af2
        -v /web:/usr/local/apache2/htdocs: volume mapping
    19. curl localhost:8081/mypage.html         //view the page
    Part 2:
        1. podman generate systemd web5 . /etc/systemd/system/web5-container.service
        2. system daemon-reload
        3. systemctl start web5-container.service
        4. systemctl status web5-container.service
        5. systemctl enable web5-container.service
        6. useradd test
        7. passwd
        8. ssh test@localhost
        9. podman pull docker.io/library/httpd
        10. podman images
        11. podman run -d --name usertest -p 8085:80 359570977af2
        12. mkdir -p ~/.config/systemd/usertest
        13. podman generate systemd usertest > ~/.config/systemd/user/usertest-container.service
        14. vi ~/.config/systemd/system/usertest/usertest-container.service
            End of line change WantedBy=default.service 
        15. systemctl --usertest daemon-reload
        16. systemctl --usertest start usertest-container
        17. systemctl --usertest enable usertest-container
        18. systemctl --usertest status usertest-container