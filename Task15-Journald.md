journalctl --no-pager | grep /log/journal | tail
    /run/log/journal/
vim /etc/systemd/journald.conf
    Storage=persistent
mkdir /var/log/journal
systemctl restart systemd-journald
journalctl --flush
verify
journalctl --no-pager | grep /log/journal | tail
    /var/log/journal
ls /var/log/journal
journalctl -b -1
    -b boot -1 one hour
    