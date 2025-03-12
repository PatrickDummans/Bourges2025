# 📌 Interface Interactive - Commandes et Combinaisons Courantes sous Linux

Ce guide répertorie les principales commandes Linux pour la navigation, la gestion des fichiers et le transfert de fichiers, y compris certaines combinaisons avancées.

---

## 🔍 Navigation et Gestion des Fichiers

| Commande | Description |
|----------|------------|
| `ls` | Liste les fichiers et dossiers du répertoire actuel |
| `ls -l` | Affiche les fichiers avec détails (permissions, taille, date de modification) |
| `ls -a` | Affiche les fichiers cachés |
| `ls -lh` | Affiche la liste des fichiers avec tailles lisibles (Ko, Mo, Go) |
| `cd <dossier>` | Se déplacer dans un dossier |
| `cd ..` | Revenir au dossier parent |
| `cd /` | Aller à la racine du système |
| `pwd` | Affiche le chemin du dossier actuel |
| `mkdir <nom_dossier>` | Créer un nouveau dossier |
| `mkdir -p <chemin/dossier>` | Créer un dossier et ses parents s’ils n’existent pas |
| `rmdir <nom_dossier>` | Supprimer un dossier vide |
| `rm -r <nom_dossier>` | Supprimer un dossier et son contenu récursivement |
| `rm -f <nom_fichier>` | Forcer la suppression d'un fichier sans confirmation |
| `rm -rf <nom_dossier>` | Supprimer un dossier et tout son contenu sans confirmation |
| `cp <fichier> <destination>` | Copier un fichier vers une destination |
| `cp -r <dossier> <destination>` | Copier un dossier et tout son contenu |
| `mv <ancien_nom> <nouveau_nom>` | Renommer ou déplacer un fichier/dossier |
| `touch <nom_fichier>` | Créer un fichier vide |
| `cat <nom_fichier>` | Afficher le contenu d’un fichier |
| `tac <nom_fichier>` | Afficher le contenu d’un fichier à l’envers |
| `head -n 10 <nom_fichier>` | Afficher les 10 premières lignes d’un fichier |
| `tail -n 10 <nom_fichier>` | Afficher les 10 dernières lignes d’un fichier |
| `tail -f <nom_fichier>` | Suivre en direct les nouvelles lignes ajoutées à un fichier |
| `find /chemin -name "*.txt"` | Rechercher des fichiers par nom |
| `find /chemin -type d` | Rechercher uniquement des dossiers |

---

## 📂 Transfert de Fichiers

| Commande | Description |
|----------|------------|
| `scp <fichier> user@hôte:/chemin/` | Copier un fichier vers un serveur distant via SSH |
| `scp -r <dossier> user@hôte:/chemin/` | Copier un dossier vers un serveur distant |
| `scp user@hôte:/chemin/fichier .` | Télécharger un fichier depuis un serveur distant |
| `rsync -avz <source> <destination>` | Synchroniser des fichiers entre deux dossiers ou machines |
| `wget <URL>` | Télécharger un fichier depuis une URL |
| `curl -O <URL>` | Télécharger un fichier avec `curl` |

---

## 🔥 Combinaisons Avancées

| Commande | Description |
|----------|------------|
| `ls -l | grep ".txt"` | Lister uniquement les fichiers `.txt` |
| `du -sh *` | Voir la taille de chaque fichier/dossier dans le répertoire actuel |
| `df -h` | Vérifier l’espace disque disponible |
| `tar -cvf archive.tar dossier/` | Créer une archive `.tar` |
| `tar -xvf archive.tar` | Extraire une archive `.tar` |
| `tar -czvf archive.tar.gz dossier/` | Créer une archive compressée `.tar.gz` |
| `tar -xzvf archive.tar.gz` | Extraire une archive `.tar.gz` |
| `zip -r archive.zip dossier/` | Compresser un dossier en `.zip` |
| `unzip archive.zip` | Décompresser une archive `.zip` |
| `chmod 755 fichier.sh` | Donner les permissions d’exécution au fichier |
| `chown user:group fichier` | Changer le propriétaire d’un fichier |
| `ps aux | grep apache` | Rechercher un processus spécifique |
| `kill -9 <PID>` | Forcer l’arrêt d’un processus |
| `history | grep "commande"` | Rechercher une commande dans l’historique |
| `echo "Hello" > fichier.txt` | Écrire dans un fichier |
| `echo "Nouvelle ligne" >> fichier.txt` | Ajouter une ligne dans un fichier |

---

📌 **Astuce** : Utilisez `man <commande>` pour afficher le manuel d’une commande.

