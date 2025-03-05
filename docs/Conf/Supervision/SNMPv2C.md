# Documentation Zabbix - Surveillance Cisco, Artica Proxy et Windows Server 2019

## 📌 Introduction
Ce document décrit la configuration et l'intégration de **Zabbix** pour surveiller :
- **Routeur Cisco 1921**
- **Switch Cisco 9200L**
- **Artica Proxy**
- **Windows Server 2019**

---

# 1️⃣ Configuration de SNMPv2c sur un Routeur Cisco 1921

## 🛠️ Étape 1 : Activer SNMPv2c
```bash
enable
configure terminal
snmp-server community ZABBIX-COMU RO
access-list 10 permit 192.168.1.100
snmp-server community ZABBIX-COMU RO 10
exit
write memory
```

## 🛠️ Étape 2 : Tester SNMP depuis Zabbix Server
```bash
snmpwalk -v 2c -c ZABBIX-COMU 192.168.1.1
```

## 🛠️ Étape 3 : Ajouter le Routeur Cisco dans Zabbix
- **Nom** : `Cisco1921`
- **IP** : `192.168.1.1`
- **Interfaces** : SNMP, Port `161`
- **Modèle recommandé** : `Template Net Cisco IOS SNMPv2`

---

# 2️⃣ Configuration de SNMPv2c sur un Switch Cisco 9200L

## 🛠️ Étape 1 : Activer SNMPv2c
```bash
enable
configure terminal
snmp-server community ZABBIX-COMU RO
access-list 10 permit 192.168.1.100
snmp-server community ZABBIX-COMU RO 10
exit
write memory
```

## 🛠️ Étape 2 : Tester SNMP
```bash
snmpwalk -v 2c -c ZABBIX-COMU 192.168.1.2
```

## 🛠️ Étape 3 : Ajouter le Switch Cisco dans Zabbix
- **Modèle recommandé** : `Template Net Cisco IOS SNMPv2`
- **Ajouter le switch** dans *Configuration* → *Hôtes* → *Interfaces SNMP*.

---

# 3️⃣ Surveillance d'Artica Proxy avec Zabbix

## 🛠️ Étape 1 : Installer l'agent Zabbix sur Artica Proxy
```bash
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-agent/zabbix-agent_6.0-1_amd64.deb
dpkg -i zabbix-agent_6.0-1_amd64.deb
nano /etc/zabbix/zabbix_agentd.conf
```
Modifier les lignes suivantes :
```
Server=192.168.1.100
ServerActive=192.168.1.100
Hostname=ArticaProxy
```
Puis redémarrer l’agent :
```bash
systemctl restart zabbix-agent
```

## 🛠️ Étape 2 : Ajouter Artica Proxy dans Zabbix
- **Modèle recommandé** : `Template App Squid SNMP`
- **Ajouter Artica Proxy** dans *Configuration* → *Hôtes* → *Interfaces SNMP*.

---

# 4️⃣ Surveillance de Windows Server 2019 avec l'Agent Zabbix

## 🛠️ Étape 1 : Installer l'agent Zabbix sur Windows Server
1. Télécharger l’agent depuis [Zabbix.com](https://www.zabbix.com/download_agents)
2. Installer le fichier `.msi` avec ces paramètres :
   - **Server** : `192.168.1.100`
   - **Hostname** : `WindowsServer2019`
3. Ouvrir le port **10050** dans le pare-feu :
   ```powershell
   New-NetFirewallRule -DisplayName "Zabbix Agent" -Direction Inbound -Protocol TCP -LocalPort 10050 -Action Allow
   ```
4. Redémarrer l'agent :
   ```powershell
   Restart-Service -Name Zabbix
   ```

## 🛠️ Étape 2 : Ajouter Windows Server 2019 dans Zabbix
- **Modèle recommandé** : `Template OS Windows by Zabbix agent`
- **Ajouter Windows Server** dans *Configuration* → *Hôtes* → *Interfaces Agent*.

---

# 5️⃣ Vérifier la version de Zabbix

## 🛠️ Méthode 1 : Depuis l'interface Web
- Allez en bas du **Tableau de bord**, la version est affichée.

## 🛠️ Méthode 2 : En ligne de commande
```bash
zabbix_server -V
```

## 🛠️ Méthode 3 : Via MySQL (si Zabbix utilise MySQL)
```bash
mysql -u zabbix -p -e "SELECT * FROM dbversion;"
```

---

# 🎯 Conclusion
✔ **Cisco 1921 & 9200L surveillés via SNMPv2c** 
✔ **Artica Proxy surveillé via l'agent Zabbix ou SNMP** 
✔ **Windows Server 2019 surveillé via l'agent Zabbix** 
✔ **Zabbix configuré et fonctionnel pour tous ces équipements** 

🚀 **Zabbix est maintenant prêt à monitorer votre infrastructure efficacement !**

