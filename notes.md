
sudo apt install python3-paramiko sshpass ansible

=========================================================================

ansible all -m raw -a "show version"
ansible all -m raw -a "show ip interface brief"
ansible all -m raw -a "show ip interface brief" -c ssh


ansible all -m ios_command -a "commands='show ip int brief'" -c network_cli
ansible all -m ios_ping -a "dest=192.168.122.1"
ansible all -m ios_ping -a "dest=192.168.122.1" -c network_cli

=====================================================================================================

# 1. Ping test
ansible all -m cisco.ios.ios_ping -a "dest=8.8.8.8"

# 2. Show clock
ansible all -m cisco.ios.ios_command -a "commands='show clock'"

# 3. Show CDP neighbors
ansible all -m cisco.ios.ios_command -a "commands='show cdp neighbors'"

# 4. Show logging
ansible all -m cisco.ios.ios_command -a "commands='show logging'"

======================================================================================================


configure terminal
hostname R2
ip domain-name example.com
crypto key generate rsa modulus 2048
username devops privilege 15 secret devops
line vty 0 4
 transport input ssh
 login local
end
write memory

==========================================================================================================

အခု စမ်းသပ်နိုင်တဲ့ အခြား commands များ
၁. Router information များ ရယူပါ

# Router version ကြည့်ပါ
ansible all -m cisco.ios.ios_command -a "commands='show version'"

# Interface status ကြည့်ပါ
ansible all -m cisco.ios.ios_command -a "commands='show ip interface brief'"

# Running configuration ကြည့်ပါ
ansible all -m cisco.ios.ios_command -a "commands='show running-config'"

===========================================================================================================

၂. Configuration ပြောင်းလဲခြင်း

# Hostname ပြောင်းပါ
ansible all -m cisco.ios.ios_config -a "lines='hostname TEST-ROUTER'"

# Banner ထည့်ပါ
ansible all -m cisco.ios.ios_config -a "lines='banner motd # This is managed by Ansible #'"

# Interface description ပြောင်းပါ
ansible all -m cisco.ios.ios_config -a "lines='description Configured by Ansible' parents='interface GigabitEthernet0/0'"


=============================================================================================================

၃. Facts ရယူပါ

# Network facts ရယူပါ
ansible all -m cisco.ios.ios_facts

# Output ကို register လုပ်ပြီး သုံးပါ
ansible all -m cisco.ios.ios_facts -a "gather_subset=all"

================================================================================================================



***optional config********



ssh -o KexAlgorithms=+diffie-hellman-group-exchange-sha1 \
    -o Ciphers=+aes128-cbc \
    -o HostKeyAlgorithms=+ssh-rsa \
    -o PubkeyAcceptedKeyTypes=+ssh-rsa \
    devops@192.168.101.101


==========================================================================    



SSH config ကို ပြင်ပါ


# ~/.ssh/config မှာ

Host 192.168.101.*
    KexAlgorithms +diffie-hellman-group-exchange-sha1
    Ciphers +aes128-cbc
    HostKeyAlgorithms +ssh-rsa
    PubkeyAcceptedKeyTypes +ssh-rsa
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null



==================================================================================================================



