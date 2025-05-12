# Switch Coeur de réseau 


## VLAN Installer sur le switch 

| ID de VM         | Nom             | Interfaces  | IP VLAN   |
| :--------------- |:---------------:| :----------:| :--------:|
| 210              |   VM-SERVE      |  Gi 1/0/1 - 4 | 172.28.64.254 |
| 211              |   VM-MANA       |  G1 1/0/5 - 6 | 192.168.0.1 |
| 219              |   VLAN-INTERCO  |  Gi 1/0/7     | 10.0.219.1 |
| 219              |   LAN - FW (Trunk) |  Gi 1/0/8     | N/D|
| N/D              |   ARUBA         |  Gi 1/0/10     | N/D |
| 215              |   VLAN - WIFI   |  X             | N/D |
| 213              |   WAN (Access)  |  Gi 1/0/21- 22 | N/D |
| 213              |   WAN (Trunk)   |  X            | N/D |
| N/D              |   DMZ (Trunk)   |  Gi 1/0/15     | N/D|
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



