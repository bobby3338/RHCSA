1. Cron
        Minutes / Hours / Day of the Month / Month / Day of Week / Command  
             
    1.  crontab -e                       //-e text editor
        0 10 4 2 * /usr/local/bin/backup  //Feb 4 10:00 backup
    2.  crontab -e -user1                // specify user
        8 12 * * Thu /bash/echo hello  //Thursday 21:08 hello
    3.  用户 natasha 必须配置一个定时任务,每天在本地时间 14:23 时执行命令
        /bin/echo hiya
        crontab -u natasha -e
        23 14 * * * /bin/echo hiya
        cat /var/spool/cron/natasha
