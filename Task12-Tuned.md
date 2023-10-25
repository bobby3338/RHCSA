Task 3:  Tuned profile in Linux 
    1. dnf install tuned
    2. systemctl enable tuned
    3. systemctl start tuned
    4. tuned-adm list                       #view options
    5. tuned-adm profile virtual-guest 
    6. important commands   
        tuned-adm recommend/active/profile/off/list