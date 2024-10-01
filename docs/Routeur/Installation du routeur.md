# Routeur CISCO

## <span style="color: white"> **Installation du Routeur** ##

Pour commencer **l'installation du routeur**, on a besoin de **reset la configuration** :

**`confreg 0x2142`**

**`reset`**

**`confreg 0x2102`**

**`reset`**

Ensuite **la configuration du port où on connectera reseau local** : 

Quand la question "**Quelle interface on souhaite choisir**", il faudra sélectionner:

**`GigabitEthernet 0/1`** (Pour notre cas)

### <span style="color: white"> **Connexion SSH** ###

Le protocole Secure Shell (SSH) permet d'établir des connexions chiffrées à distance entre des ordinateurs. Il permet également la tunnellisation. Pour effectuer cette installation: 

``` 
Router> enable
Router# configure terminal
Router(config)# hostname BRG-R(N* du Routeur)
Router(config)# ip domain-name exemple.com
Router(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
Router(config)# ip ssh version 2
Router(config)# username admin privilege 15 secret MonMotDePasse
Router(config)# line vty 0 4
Router(config-line)# login local
Router(config-line)# transport input ssh
Router(config-line)# exec-timeout 5 0
Router(config-line)# exit
Router# write memory
``` 
### <span style="color: white"> **Configuration des interfaces des routeurs** ###

**R1**

```
-------- PARTIE WAN -------- 
interface GigabitEthernet0/0
 ip address 221.87.118.2 255.255.255.252
 ip nat outside
 ip virtual-reassembly in
 duplex auto
 speed auto
!
-------- PARTIE LAN --------
interface GigabitEthernet0/1
 no ip address
 ip nat inside
 ip virtual-reassembly in
 duplex auto
 speed auto
!

-------- Configuration des interfaces virtuelles --------

interface GigabitEthernet0/1.211
 encapsulation dot1Q 211
 ip address 192.168.0.253 255.255.255.0
!
interface GigabitEthernet0/1.212
 encapsulation dot1Q 213
 ip address 192.168.255.253 255.255.255.128
 ip nat inside
 ip virtual-reassembly in
 standby 10 ip 192.168.255.254
 standby 10 preempt
```

**R2**
```
-------- PARTIE WAN -------- 
interface GigabitEthernet0/0
 ip address 221.87.118.2 255.255.255.252
 ip nat outside
 ip virtual-reassembly in
 duplex auto
 speed auto
!
-------- PARTIE LAN --------
interface GigabitEthernet0/1
 no ip address
 ip nat inside
 ip virtual-reassembly in
 duplex auto
 speed auto
!
-------- Configuration des interfaces virtuelles --------
interface GigabitEthernet0/1.211
 encapsulation dot1Q 211
 ip address 192.168.0.252 255.255.255.0
!
interface GigabitEthernet0/1.212
 encapsulation dot1Q 213
 ip address 192.168.255.252 255.255.255.128
 ip nat inside
 ip virtual-reassembly in
 standby 10 ip 192.168.255.254
 standby 10 preempt
```
**`BIEN METTRE LA COMMANDE "ip nat inside" SUR L'INTERFACE PHYSIQUE DE LA PARTIE LAN ET EGALEMENT SUR L'INTERFACE VIRTUELLE `**

### <span style="color: white"> **Configuration des routes sur les routeurs** ###

**R1**
```
-------- ROUTE DE SORTIE -------- 
Router> enable
Router# configure terminal
Router# ip route 0.0.0.0 0.0.0.0 183.44.18.2

-------- ROUTE DE RETOUR --------
Router> enable
Router# configure terminal
Router# ip route 172.28.0.0 255.255.0.0 192.168.255.129
Router# ip route 192.168.255.0 255.255.255.128 192.168.255.129

```
**R2**
```
-------- ROUTE DE SORTIE -------- 
Router> enable
Router# configure terminal
Router# ip route 0.0.0.0 0.0.0.0 221.87.118.1

-------- ROUTE DE RETOUR --------
Router> enable
Router# configure terminal
Router# ip route 172.28.0.0 255.255.0.0 192.168.255.129
Router# ip route 192.168.255.0 255.255.255.128 192.168.255.129

```

