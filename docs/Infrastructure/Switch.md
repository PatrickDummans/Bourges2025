# Switch Coeur de réseau 


## VLAN Installer sur le switch 

| ID de VM         | Nom             | Interfaces  | IP VLAN   |
| :--------------- |:---------------:| :----------:| :--------:|
| 210              |   VM-SERVE      |  Gi 1/0/1 - 4 | 172.28.64.254 |
| 211              |   VM-MANA       |  G1 1/0/5 - 6 | 192.168.0.1 |
| 219              |   LAN           |  Gi 1/0/7 - 10 | 10.0.219.1 |
| 219              |   LAN (Trunk)   |  Gi 1/0/9     | N/D|
| 213              |   WAN (Access)  |  Gi 1/0/21- 22 | N/D |
| 213              |   WAN (Trunk)   |  Gi 1/0/23- 24 | N/D |
| 217              |   VLAN-CONDI    |  Gi 1/0/15 - 16 | 172.28.80.254 |
| 218              |   VLAN-LOG      |  Gi 1/0/17 - 18 | 172.28.81.254 |
| 212              |   VLAN-LIVR     |  Gi 1/0/19 - 20 | 172.28.82.254 |



## VM Linux & Windows server

| ID de VLAN       | Nom De la VM     | LOGS                      | IP          |
| :--------------- |:---------------: | :------------------------ | :------------
| 210              |   BRG_LIN_CLONE  |  Passw0rd123456! / admin  | 172.28.64.3 |
| 211              |   BRG_WINSERV2019|  P@ssw0rd123456! / admin  | 172.28.64.2 |

