# Switch Coeur de réseau 


## VLAN Installer sur le switch 

| ID de VM         | Nom             | Interfaces  | IP    |
| :--------------- |:---------------:| :----------:| :--------:|
| 210              |   VM-SERVE      |  Gi 1/0/1 - 2 | 172.28.64.254 |
| 211              |   VM-MANA      |  G1 1/0/3 - 6 | 192.168.0.1 |
| 212              |   LAN           |  Gi 1/0/7 - 10 | 172.28.70.254 |
| 213              |   WAN           |  Gi 1/0/11 - 14 | 172.28.72.254 |
| 217              |   VLAN-CONDI    |  Gi 1/0/15 - 16 | 172.28.80.254 |
| 218              |   VLAN-LOG      |  Gi 1/0/17 - 18 | 172.28.81.254 |
| 219              |   VLAN-LIVR     |  Gi 1/0/19 - 20 | 172.28.82.254 |



## VM Linux & Windows server

| ID de VLAN       | Nom De la VM     | LOGS                      | IP          |
| :--------------- |:---------------: | :------------------------ | :------------
| 210              |   BRG_LIN_CLONE  |  Passw0rd123456! / admin  | 172.28.64.3 |
| 211              |   BRG_WINSERV2019|  P@ssw0rd123456! / admin  | 172.28.64.2 |