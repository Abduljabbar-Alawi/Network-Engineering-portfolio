
# 🛠️ SW1 Switch Configuration (Clean)

This file contains the sanitized configuration for SW1, including VLANs, 802.1Q Trunking, STP PortFast, and SSH access.

### 1. Baseline Security & SSH
```cisco
hostname SW1
no ip domain-lookup
ip domain-name netsec.com
service password-encryption
enable algorithm-type scrypt secret <REDACTED_SECRET_HASH>
username admin privilege 15 secret <REDACTED_SECRET_HASH>

line con 0
 logging synchronous
 login local
line vty 0 4
 logging synchronous
 login local
 transport input ssh
```

### 2. VLAN Configuration
```cisco
vlan 10
 name SALES
vlan 20
 name HR
```

### 3. Interfaces (Trunk & Access with STP Security)
```cisco
interface GigabitEthernet0/0
 description TRUNK_TO_R1
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk

interface GigabitEthernet0/1
 description PC_SALES
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast edge

interface GigabitEthernet0/2
 description PC_HR
 switchport access vlan 20
 switchport mode access
 spanning-tree portfast edge
```
