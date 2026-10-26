
# 🛠️ SW3 Switch Configuration (Access)

This file contains the sanitized configuration for SW3, including LACP EtherChannel and STP Security.

### 1. Baseline Security & SSH
```cisco
hostname SW3-Access
no ip domain-lookup
ip domain-name netsec.com
service password-encryption
enable secret 9 $9$uwYBDj8YqaboH9$IP.0JX3FSY0d513MxU.V.CFJNb2xtHRyhv01gi2KHE.
username admin privilege 15 secret 5 $1$BYIs$d0.0Mwq.jMvv/zAx2/wp/.
banner motd # Unauthorized Access Prohibited! #
no ip http server
no ip http secure-server

line con 0
 logging synchronous
 login local
line vty 0 4
 logging synchronous
 login local
 transport input ssh
```

### 2. Interfaces & LACP
```cisco
interface Port-channel1
 description LACP_TO_SW2
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk

interface GigabitEthernet0/0
 description TRUNK_TO_SW1
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk

interface GigabitEthernet0/1
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 1 mode active

interface GigabitEthernet0/2
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 1 mode active
```

### 3. Access Ports & STP Security
```cisco
interface GigabitEthernet0/3
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast edge
 spanning-tree bpduguard enable

interface GigabitEthernet1/0
 switchport access vlan 20
 switchport mode access
 spanning-tree portfast edge
 spanning-tree bpduguard enable
```
