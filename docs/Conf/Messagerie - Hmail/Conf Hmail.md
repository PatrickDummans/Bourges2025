# 📧 Installation et Configuration de HmailServer

## 🔧 1. Prérequis

- 💻 **Système** : Windows 10 (machine virtuelle ou physique)
- 📦 **Composant requis** : [.NET Framework 2.0](https://www.microsoft.com/fr-fr/download/details.aspx?id=6041&msockid=1f28469026956a1305a253bd27016bc2)
- 🌐 Accès Internet pour le téléchargement des paquets

---

## 🚀 2. Installation de HmailServer

### Étapes :

```bash
# 1. Télécharger la dernière version de HmailServer
Naviguer vers : https://www.hmailserver.com/download/

# 2. Lancer le fichier d’installation téléchargé

# 3. Suivre les instructions de l’assistant d’installation :
- Cliquer sur **Suivant** jusqu’à la section des composants
- Choisir une **installation complète** (Full Installation) :
  - ✅ Server
  - ✅ Administrative Tools
- Pour la base de données, sélectionner : **Microsoft SQL Compact**
- Choisir l’emplacement de création du raccourci HmailServer
- Définir un mot de passe d’administration sécurisé

# 4. Installation du .NET Framework 2.0
⚠️ Si une erreur survient à ce stade concernant le Framework .NET :
- Installer **manuellement** la version 2.0 avant de continuer

# 5. Finalisation
- Fermer l’installeur
- HmailServer se lance automatiquement à la fin de l’installation
```

---

## ⚙️ 3. Configuration de HmailServer

### 🔐 Connexion

- Lancer HmailServer Administrator
- Saisir le mot de passe défini lors de l’installation

---

### 🌐 Création d’un Domaine

1. Aller dans `Domains`
2. Cliquer sur `Add`
3. Renseigner le domaine :  
   **mail.bourges.sportludique.fr**

![Domain](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/domain.png)

---

### 👥 Création de Comptes Utilisateurs

1. Naviguer vers `Accounts`
2. Cliquer sur `Add`
3. Créer deux adresses mail en définissant leurs mots de passe

![Comptes](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/comptes.png)

---

### 🚫 Désactiver l’AutoBan

1. Aller dans `Settings > Advanced > Auto-ban`
2. **Décocher** l’option `Enabled`

![Autoban](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/autoban.png)

---

## 🔐 4. Configuration du Pare-feu

### 📤 Trafic SMTP (Ports 25 et 587)

1. Ouvrir le **Pare-feu Windows Defender avec fonctions avancées de sécurité**
2. Dans **Règles de trafic entrant**, localiser ou créer une règle pour **SMTP**
3. S’assurer que les **ports TCP 25 et 587** sont bien autorisés

![Pare-feu SMTP](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Parefeu%20SMTP.png)

---

### 📥 Trafic IMAP (Port 143)

1. Dans le Pare-feu Windows Defender :
2. Accéder aux **propriétés de IMAP**
3. Sous l’onglet **Protocoles et Ports** :
   - Port local : **143**
   - Port distant : **Tous les ports**

![ParfeuIMAP](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/ParefeuIMAP.png)

---

## 📬 5. Configuration du Client Mail (Thunderbird)

1. Ajouter un compte mail dans Thunderbird
2. Aller dans les **paramètres du compte**
3. Modifier le **serveur SMTP** :
   - Nom du serveur : **mail.bourges.sportludique.fr**
   - Port : **587**

![ServerSMTP](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Param%C3%A8tres.png)

---

## ✅ 6. Vérification via Diagnostics

1. Aller dans le menu `Utilities > Diagnostics`
2. Sélectionner le domaine : **mail.bourges.sportludique.fr**
3. Lancer le test de diagnostic

![Diagnostique](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads)

---

💡 **Astuce** : Vérifiez la connectivité SMTP/IMAP depuis l’extérieur à l’aide d’un outil tel que [MXToolbox](https://mxtoolbox.com/) pour un test complet du serveur mail.


