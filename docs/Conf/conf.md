
# Conf


## Switch 

``` 
# Config des VLAN 

enable
configure terminal
vlan 211
name VLAN-MANA
exit
vlan 210
name VLAN-SERVE
exit

interface range Gi1/0/1 - 2
switchport mode access
switchport access vlan 211
exit

interface range Gi1/0/3 - 4
switchport mode access
switchport access vlan 210
exit

interface vlan 211
ip address 192.168.0.1 255.255.255.0
no shutdown
exit

interface vlan 210
ip address 172.28.64.254 255.255.255.0
no shutdown
exit

write memory

# show vlan brief (pour voir les vlan et les port affecter a ses derniers)
# show ip interface brief (ip affecter au vlan)
```
```
interface GigabitEthernet0/0
 vrf forwarding Mgmt-vrf
 no ip address
 shutdown
!
interface GigabitEthernet1/0/1
 switchport access vlan 210
 switchport mode access
!
interface GigabitEthernet1/0/2
 switchport access vlan 210
 switchport mode access
!
interface GigabitEthernet1/0/3
 switchport access vlan 210
 switchport mode access
!
interface GigabitEthernet1/0/4
 switchport access vlan 210
 switchport mode access
!         
interface GigabitEthernet1/0/5
 switchport access vlan 211
 switchport mode access
!
interface GigabitEthernet1/0/6
 switchport access vlan 211
 switchport mode access
!
interface GigabitEthernet1/0/7
 switchport access vlan 219
 switchport mode access
!
interface GigabitEthernet1/0/8
 switchport access vlan 212
 switchport mode access
!
interface GigabitEthernet1/0/9
 switchport trunk allowed vlan 211,219
 switchport mode trunk
!
interface GigabitEthernet1/0/10
 switchport access vlan 212
 switchport mode access
!
interface GigabitEthernet1/0/21
 switchport access vlan 213
 switchport mode access
!
interface GigabitEthernet1/0/22
 switchport access vlan 213
 switchport mode access
!
interface GigabitEthernet1/0/23
 switchport trunk allowed vlan 211-213
 switchport mode trunk
!
interface GigabitEthernet1/0/24
 switchport trunk allowed vlan 211-213
 switchport mode trunk
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan210
 ip address 172.28.64.254 255.255.255.0
!
interface Vlan211
 ip address 192.168.0.1 255.255.255.0
!
interface Vlan212
 no ip address
!
interface Vlan219
 ip address 10.0.219.1 255.255.255.0
!
ip default-gateway 192.168.255.126
ip forward-protocol nd
ip http server
ip http authentication local
ip http secure-server
ip route 0.0.0.0 0.0.0.0 10.0.219.254
ip ssh time-out 60
ip ssh version 2
```

##  Router 

```
