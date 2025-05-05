# 🛡️ Intégration d'un Antivirus Externe dans hMailServer v5.6

## 🔧 1. Prérequis

- **Version de hMailServer** : 5.6 ou supérieure
- **Système d'exploitation** : Windows (compatible avec hMailServer)
- **Antivirus** : Doit prendre en charge l'analyse en ligne de commande
- **Accès administrateur** : Requis pour modifier la configuration de hMailServer

## ⚙️ 2. Configuration d'un Antivirus Externe

### Étapes :

1. **Lancer l'Administrateur hMailServer** :
   - Ouvrir l'application *hMailServer Administrator*.

2. **Naviguer vers les paramètres de l'antivirus** :
   - Aller dans `Settings` → `Protocols` → `SMTP` → `AntiVirus`.

3. **Activer l'analyse externe** :
   - Sélectionner l'onglet `External virus scanner`.
   - Cocher l'option `Use external scanner`.

4. **Définir la ligne de commande de l'antivirus** :
   - Dans le champ `Scanner executable`, entrer la commande suivante (inclure les guillemets) :
     ```bash
     "C:\Program Files\Grisoft\AVG Free\avgscan.exe" /EXT=* /NOBOOT /NOMEM /SCAN /NOSELF /NOHIMEM /ARC "%FILE%"
     ```
     - Remplacer le chemin par celui de votre antivirus si différent.
     - `%FILE%` est une macro remplacée par le chemin du fichier à analyser.

5. **Spécifier la valeur de retour en cas de détection de virus** :
   - Dans le champ `Return value`, entrer :
     ```bash
     6
     ```
     - Pour `avgscan.exe`, une valeur de retour de `6` indique qu'un virus a été trouvé.

6. **Définir le comportement en cas de détection** :
   - Choisir entre :
     - `Delete e-mail` : Supprimer l'e-mail contenant un virus.
     - `Delete attachments` : Supprimer uniquement les pièces jointes infectées.
   - Optionnellement, activer les notifications pour l'expéditeur et/ou le destinataire.

7. **Enregistrer la configuration** :
   - Cliquer sur `Save` pour appliquer les modifications.

## 🧪 3. Test de l'Intégration

### Utilisation du fichier de test EICAR :

- Le fichier EICAR est une chaîne de test reconnue par les antivirus comme un virus, mais inoffensive.
- Pour tester l'intégration :
  1. Télécharger le fichier de test EICAR depuis un site fiable.
  2. Envoyer un email contenant le fichier EICAR en pièce jointe à une adresse gérée par hMailServer.
  3. Vérifier que l'email est bloqué ou que l'action configurée est exécutée.

## 📝 Remarques

- **Macro `%FILE%`** : Assurez-vous que votre antivirus supporte la substitution de `%FILE%` par le chemin du fichier à analyser.
- **Valeur de retour** : La valeur de retour indiquant la détection d'un virus varie selon l'antivirus utilisé. Consultez la documentation de votre antivirus pour déterminer la valeur appropriée.
- **Sécurité** : Toujours tester avec des fichiers de test comme EICAR pour éviter tout risque d'infection.

## 📚 Références

- Documentation officielle de hMailServer : [Anti virus](https://www.hmailserver.com/documentation/v5.6/?page=reference_antivirus)

