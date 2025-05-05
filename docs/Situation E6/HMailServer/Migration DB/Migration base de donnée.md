# 📦 Procédure de Migration de la Base de Données HMailServer vers une Nouvelle Machine Virtuelle

## 🎯 Objectif
Migrer la base de données utilisée par **HMailServer** vers une **nouvelle machine virtuelle dédiée** à l’hébergement de bases de données, tout en garantissant la **continuité du service de messagerie**.

---

## 🔧 1. Pré-requis

### ✅ Techniques
- Serveur HMailServer existant et fonctionnel
- Accès administrateur aux deux machines (source et cible)
- Moteur de base de données installé (MySQL ou SQL Server)
- Outils d’administration : `mysqldump`, **SQL Server Management Studio (SSMS)**, etc.

### 🔐 Réseau & Sécurité
- Connexion réseau stable entre les deux machines
- Ouverture des ports nécessaires (ex. : `3306` pour MySQL)
- Droits d'accès à distance pour l’utilisateur de la base de données

---

## 🖥️ 2. Création de la Machine Virtuelle

1. Créer une nouvelle VM avec un **OS compatible** (Windows Server recommandé)
2. Installer les **mises à jour système**
3. Installer le **moteur de base de données** (MySQL ou SQL Server)
4. Configurer le **pare-feu** pour autoriser les connexions entrantes à ce moteur

---

## 💾 3. Export de la Base de Données Existante

### Pour **MySQL** :
```bash
mysqldump -u [utilisateur] -p hmailserver > hmailserver_backup.sql
```

### Pour **SQL Server** :
- Ouvrir **SQL Server Management Studio**
- Clic droit sur la base `hmailserver`
- Aller dans **Tasks → Back Up** ou **Generate Scripts**

---

## 📥 4. Import de la Base sur la Nouvelle VM

### Pour **MySQL** :
```bash
mysql -u [utilisateur] -p
CREATE DATABASE hmailserver;
exit
mysql -u [utilisateur] -p hmailserver < hmailserver_backup.sql
```

### Pour **SQL Server** :
- Utiliser l’interface graphique de SSMS
- Ou exécuter un **script SQL** de restauration

---

## 👤 5. Création des Utilisateurs et Configuration des Accès

- Créer un utilisateur avec **droits complets** sur la base `hmailserver`
- Vérifier les **droits de connexion à distance**
- Ouvrir les **ports réseau nécessaires** sur le pare-feu (ex. : `3306`)

---

## 🛠️ 6. Reconfiguration de HMailServer

### Modifier le fichier `hMailServer.ini` :
**Chemin par défaut** :
```
C:\Program Files (x86)\hMailServer\Bin\hMailServer.ini
```

### Adapter les paramètres suivants :
```ini
[Database]
Type=MYSQL
Username=hmail
Password=*******
PasswordEncryption=1
Database=hmailserver
Server=IP_ou_Nom_DNS_VM
```

### Redémarrer le service HMailServer :
```powershell
Restart-Service hMailServer
```

---

## ✅ 7. Vérifications Post-Migration

- Consulter les **logs de connexion** :
  ```
  C:\Program Files (x86)\hMailServer\Logs\
  ```
- Tester l’**envoi/réception d’e-mails**
- Vérifier que les **nouveaux messages** sont bien enregistrés dans la base distante
- **Désactiver l’ancienne base** après validation complète

---

## 📂 Option : Migration des Fichiers de Données

Si les messages sont stockés localement :

1. Copier le dossier `Data` :
   ```
   C:\Program Files (x86)\hMailServer\Data
   ```
   vers un **espace réseau** ou la **nouvelle VM**

2. Adapter la variable `DataFolder` dans `hMailServer.ini` si nécessaire :
```ini
[Directories]
DataFolder=nouveau_chemin_data
```
---
```

