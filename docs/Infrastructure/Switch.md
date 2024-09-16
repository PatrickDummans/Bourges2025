# Switch Coeur de réseau 


## VLAN Installer sur le switch 

| ID de VM         | Nom             | Interfaces  |
| :--------------- |:---------------:| -----:|
| 210              |   VM-MANA       |  Gi 1/0/1 - 2 |
| 211              |   VM-SERV       |  G1 1/0/3 - 6 |
| 212              |   LAN           |  Gi 1/0/7 - 10 |
| 213              |   WAN           |  Gi 1/0/11 - 14 |
| 217              |   VLAN-CONDI    |  Gi 1/0/15 - 16 |
| 218              |   VLAN-LOG      |  Gi 1/0/17 - 18 |
| 219              |   VLAN-LIVR     |  Gi 1/0/19 - 20 |



## VM Linux & Windows server

| ID de VLAN       | Nom De la VM    | LOGS  | IP   |
| :--------------- |:---------------:| -----:|-----:
| 210              |   BRG_LIN_CLONE      |  Passw0rd123456! / admin | 172.28.64.3 |
| 211              |   BRG_WINSERV2019    |  P@ssw0rd123456! / admin | 172.28.64.2 |