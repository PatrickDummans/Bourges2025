# Configuration de HmailServer 

### Installer HmailServer

**Prérequis :** VM Windows 10, .Net Framework 2.0 (https://www.microsoft.com/fr-fr/download/details.aspx?id=6041&msockid=1f28469026956a1305a253bd27016bc2).

1. Télécharger la dernière version de hmailserver à partir du lien ci-dessous :
- https://www.hmailserver.com/download/

2. Lancer l'installeur 

3. Pour l'installation, on s'appuie sur la doc ci-dessous : 
- https://www.hmailserver.com/documentation/latest/?page=howto_install


- Faire suivant jusqu'à ce que l'on vous demande de choisir les **composants** à installer, dans notre cas, nous allons faire une **full installation** c'est-à-dire installer le **server** et **l'administrative tools**. Voir le screenshot ci-dessous : 

- Choisir le type de base de données, dans notre cas, ce sera Microsoft SQL Compact.

- Choisir où HmailServer créera son raccourci.

- Définir le mot de passe pour HmailServer.

4. Premier problème ! On nous demande d'installer le .Net Framework 2.0. Si on essaye de faire installer le framework à l'installeur, il y aura une erreur, il faut donc au préalable installer ce framework. 

- Tout ceci fait, une fois que l'installation est terminée, il vous suffit de fermer l'installeur une fois que tout est fini, et HmailServer se lancera automatiquement.

### Configurer Hmailserver 

1. Se connecter et entrer le mdp 

2. Création du domaine 
- Cliquer sur domains, ensuite sur add, et créer le domaine ; dans notre cas, ce sera **mail.bourges.sportludique.fr** 

![Domain](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/domain.png)

3. Créer des comptes 
- Cliquer sur account, puis sur Add, et créer 2 mails en définissant les mots de passe qui vont avec

![Comptes](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/comptes.png)

4. Désactiver l'autoban 
- Dans settings, puis Advanced et Autoban 
- Décocher la case Enabled

![Autoban](https://github.com/PatrickDummans/Bourges2025/blob/main/images/autoban.png)

5. Vérifier si tout fonctionne convenablement
- Aller dans Utilities et cliquer sur Diagnostics 
- Sélectionner le domaine à tester, donc mail.bourges... 
- Lancer le diagnostic 

![Diagnostique](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads
