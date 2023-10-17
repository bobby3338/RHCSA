Grep
    1. grep -i "root" /etc/passwd
    2. grep "sbin" /etc/passed > /tmp/pass
Find 
    mkdir -p /root/findfiles
        -p make parent directory
    find / -user redhat -exec cp -rp {} /root/findfiles \;
        find / initiate a search starting from root/, cp -rp {} copy -r recursively -p preserve file permission {} each files or directory found.
 查找一个字符串
    a)在文件/usr/share/xml/iso-codes/iso_639_3.xml 中查找到所有包含字符 ng 的行
    b)将找出的行按照先后顺序复制到/root/list 文件中。/root/list 文件不要包含空行
    c)其中的所有行的内容必须时源文件中原始的标准副本
        sed 's/^\ //g'  //sed stream editior 
        sed 's/^\t //g' 