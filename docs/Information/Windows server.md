# 🧾 Documentation d’Infrastructure Active Directory & Partage de Fichiers

## 🖥️ 1. Informations Générales

### 🔧 Serveur Active Directory
- **Nom du domaine** : `lan.bourges.sportludique`
- **Adresse IP** :
  - `172.28.64.2/24` (VLAN Server - ID: 210)
  - `192.168.0.2/24` (VLAN MANA - ID: 211)
- **Rôle principal** : Contrôleur de domaine Windows Server avec gestion Active Directory.

---

## 👤 2. Structure Active Directory

### 📁 Unité d'organisation : `Administrateurs`
Contient :
- Utilisateurs :
  - `Admin MANAGEMENT`
  - `Patrick DUMANS`
  - `Yann MALUNGU`
- Groupes :
  - `Support_IT` (Groupe de distribution)
  - `WAdministrateur` (Groupe de sécurité)
- Sous-UO :
  - `Fichier` ➜ contient l'utilisateur `admin-srvfic` (voir section 3)

### 📁 Unité d'organisation : `Organisation`
Contient 3 sous-UO représentant les services :
- `Conditionnement`
- `Logistique`
- `Transport`

---

## 💾 3. Serveur de Fichiers

### 🔹 Nom de la machine : `BRG-SRVFIC`
- **Adresse IP** :
  - `172.28.64.60/24` (VLAN Server - ID: 210)
  - `192.168.0.60/24` (VLAN MANA - ID: 211)
- **Utilisateur spécifique** : `admin-srvfic` (lié à l’UO `Fichier` du domaine)

### 📁 Dossier partagé : `DDT`
- **Chemin réseau** : `\\Desktop-ve8olo\ddt` (également accessible via IP)
- **Type de partage** : Partage standard avec option de partage avancé disponible.

#### 📂 Accès depuis un poste Windows
```bash
\\192.168.0.60\ddt
```

#### 🐧 Accès depuis une machine Linux avec `smbclient`
```bash
smbclient //172.28.64.60/DDT -U 'LAN.BOURGES.SPORTLUDIQUE.FR\adminsrvfic' --max-protocol=SMB3
```

---

## 🛠️ 4. Résumé VLAN et IP

| Composant           | IP VLAN Server (210) | IP VLAN MANA (211) |
|---------------------|----------------------|---------------------|
| AD (DC) Server      | 172.28.64.2          | 192.168.0.2         |
| Fichier (BRG-SRVFIC)| 172.28.64.60         | 192.168.0.60        |

---

## 📌 5. Remarques
- Toutes les unités organisationnelles sont bien structurées par rôle ou service.
- Les utilisateurs sont répartis dans des UO pertinentes facilitant la gestion des droits.
- Le serveur de fichiers est séparé du contrôleur de domaine, ce qui est une bonne pratique de sécurité.
- Le partage du dossier `DDT` peut être affiné avec des permissions spécifiques par utilisateur ou groupe.
```

