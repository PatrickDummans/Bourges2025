# 📌 Guide d'installation de Zabbix 7.x sur Debian 12

## 📖 Introduction  
Ce guide détaille l'installation de **Zabbix 7.x** sur **Debian 12**, incluant la configuration du serveur, de la base de données et de l'interface web.

## 🔹 1. Mise à jour du système  
Avant de commencer, il est recommandé de mettre à jour le système : 
```bash
sudo apt update && sudo apt upgrade -y
```

## 🔹 2. Installation des prérequis  
Installer les outils nécessaires pour gérer les dépôts et dépendances : 
```bash
sudo apt install -y wget curl gnupg2 lsb-release
```

## 🔹 3. Ajout du dépôt officiel de Zabbix  
```bash
wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-1+debian12_all.deb
sudo dpkg -i zabbix-release_7.0-1+debian12_all.deb
sudo apt update
```

## 🔹 4. Installation des paquets Zabbix  
```bash
sudo apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent mariadb-server
```

## 🔹 5. Configuration de la base de données  
```bash
sudo systemctl enable --now mariadb
sudo mysql_secure_installation
```
Puis, dans MySQL : 
```sql
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'MonMotDePasseSecurisé';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
⚠️ **Remplace `MonMotDePasseSecurisé` par un mot de passe fort !** 

## 🔹 6. Importation du schéma de base de données  
```bash
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -p zabbix
```

## 🔹 7. Configuration de Zabbix Server  
```bash
sudo nano /etc/zabbix/zabbix_server.conf
```
Modifier ces lignes : 
```ini
DBHost=localhost
DBName=zabbix
DBUser=zabbix
DBPassword=MonMotDePasseSecurisé
```

## 🔹 8. Configuration de PHP pour Zabbix  
```bash
sudo nano /etc/zabbix/apache.conf
```
Vérifier ou modifier la ligne : 
```apache
php_value date.timezone Europe/Paris
```
Puis redémarrer Apache : 
```bash
sudo systemctl restart apache2
```

## 🔹 9. Démarrage et activation des services  
```bash
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
```

## 🔹 10. Configuration du pare-feu  
```bash
sudo ufw allow 80/tcp
sudo ufw allow 10051/tcp
sudo ufw allow 10050/tcp
sudo ufw reload
```

## 🔹 11. Accès à l’interface web Zabbix  
Ouvrir un navigateur et accéder à : 
```
http://<IP_DU_SERVEUR>/zabbix
```
Trouver l’IP avec : 
```bash
ip a
```

## 🔹 12. Configuration initiale de Zabbix via l’interface web  
1. **Choisir la langue** → Suivant 
2. **Vérification des prérequis** → Suivant 
3. **Configuration de la base de données** : 
   - **DBHost** : `localhost` 
   - **DBName** : `zabbix` 
   - **DBUser** : `zabbix` 
   - **DBPassword** : `MonMotDePasseSecurisé` 
   → Suivant 
4. **Configurer les paramètres du serveur** → Suivant 
5. **Résumé de la configuration** → Terminer 
6. **Se connecter avec les identifiants par défaut** : 
   - **Utilisateur** : `Admin` 
   - **Mot de passe** : `zabbix` 

## 🎯 Vérifications et dépannage  

### 🔹 Vérifier que Zabbix écoute sur le bon port  
```bash
sudo ss -tulnp | grep zabbix
```

### 🔹 Vérifier l’état des services  
```bash
sudo systemctl status zabbix-server zabbix-agent apache2
```

### 🔹 Vérifier les logs en cas de problème  
```bash
sudo tail -f /var/log/zabbix/zabbix_server.log
sudo tail -f /var/log/zabbix/zabbix_agentd.log
```

## 🎉 Conclusion  
Ton serveur **Zabbix 7.x** est maintenant installé et prêt à l'emploi ! 🚀 
📌 **Prochaine étape** : Ajouter des hôtes Linux, Windows et équipements réseau à superviser.

