# Switch Coeur de réseau 


## VLAN Installer sur le switch 

| ID de VM         | Nom             | Interfaces  | IP VLAN   |
| :--------------- |:---------------:| :----------:| :--------:|
| 210              |   VM-SERVE      |  Gi 1/0/1 - 4 | 172.28.64.254 |
| 211              |   VM-MANA       |  G1 1/0/5 - 6 | 192.168.0.1 |
| 219              |   VLAN-INTERCO  |  Gi 1/0/7     | 10.0.219.1 |
| 215              |   VLAN - WIFI   |  X             | N/D |
| 213              |   WAN (Access)  |  Gi 1/0/21- 22 | N/D |
| 217              |   VLAN-CONDI    |  Gi 1/0/23 - 24 | 172.28.80.254 |
| 218              |   VLAN-LOG      |  X              | 172.28.81.254 |
| 216              |   VLAN-LIVR     |  X              | 172.28.82.254 |



## VM Linux & Windows server

| ID de VLAN       | Nom De la VM     | LOGS                      | IP          |
| :--------------- |:---------------: | :------------------------ | :------------
| 210              |   BRG_LIN_CLONE  |  Passw0rd123456! / admin  | 172.28.64.3 |
| 211              |   BRG_WINSERV2019|  P@ssw0rd123456! / admin  | 172.28.64.2 |
| 214              |   BRG_HTTP       |  Passw0rd123456! / admin  | 192.168.18.3|
| 212              |   BRG_MARIADB    |  Passw0rd123456! / admin  | 192.168.20.3|
| 212              |   BRG_LIN_DNS    |  Passw0rd123456! / admin  | 192.168.20.2|


## Les Ports Trunk 802.1Q

| Port             | Nom             | VLAN taggés                      |
| :--------------- |:---------------:| :-----------------------------:  |
|    Gi1/0/8       | LAN - FW        | 10 / 211 / 219                   |
|    Gi1/0/10      | ARUBA           | 10 / 210 / 211 / 215 / 217 / 218 |
|    Gi1/0/15      | DMZ             | 10 / 212 / 214                   |

| Port             | Mode            | Encapsulation             | IP          | Native vlan |
| :--------------- || :-------------:|:-------------------------:|:-----------:|:-----------:|
| Gi1/0/8          | On              | 802.1q                    | trunking    | 1           |
| Gi1/0/10         | On              | 802.1q                    | trunking    | 210         |
| Gi1/0/15         | On              | 802.1q                    | trunking    | 1           |

 


