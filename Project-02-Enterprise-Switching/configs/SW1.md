
# 🛠️ SW1 Switch Configuration (Root Bridge)

This file contains the sanitized configuration for SW1, which acts as the Root Bridge.

### 1. Baseline Security & SSH
```cisco
hostname SW1-Root-bridge
no ip domain-lookup
ip domain-name netsec.com
service password-encryption
enable secret <REDACTED_SECRET_HASH>
username admin privilege 15 secret <REDACTED_SECRET_HASH>
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

### 2. STP Root Bridge Configuration
```cisco
spanning-tree mode pvst
spanning-tree vlan 10,20 priority 24576
```

### 3. Interface Configuration (Trunks)
```cisco
interface GigabitEthernet0/0
 description TRUNK_TO_SW2
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk

interface GigabitEthernet0/1
 description TRUNK_TO_SW3
 switchport trunk allowed vlan 10,20
 switchport trunk encapsulation dot1q
 switchport mode trunk
```
