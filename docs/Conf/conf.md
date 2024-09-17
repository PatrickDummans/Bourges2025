
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