# 📧 Configuration Anti-Spam de hMailServer v5.6

Ce guide détaille les fonctionnalités anti-spam intégrées de hMailServer v5.6 et fournit des instructions pour leur configuration optimale.

---

## 🔧 1. Accès aux Paramètres Anti-Spam

1. Ouvrez **hMailServer Administrator**.
2. Naviguez vers :  
   `Settings > Anti-spam`

---

## 🛡️ 2. Tests Anti-Spam Disponibles

hMailServer propose plusieurs tests pour évaluer les messages entrants :

- **Use SPF** : Vérifie si le serveur expéditeur est autorisé à envoyer des emails pour le domaine.
- **Check that sender has DNS-MX records** : Confirme l'existence d'enregistrements MX pour le domaine de l'expéditeur.
- **Check that sender has DNS-A record** : Vérifie la présence d'un enregistrement A pour le domaine de l'expéditeur.
- **Verify DKIM signature** : Valide la signature DKIM du message.
- **Check HELO host** : Analyse la commande HELO/EHLO utilisée par le serveur expéditeur.
- **Check that the host is not in DNS blacklist** : Consulte des listes noires DNSBL pour détecter les serveurs connus pour envoyer du spam.
- **Check that the sender is not in SURBL** : Vérifie si des liens dans le message pointent vers des domaines répertoriés dans des listes noires SURBL.
- **Check that the message has a valid SPF record** : Confirme la validité de l'enregistrement SPF du domaine expéditeur.

> 💡 **Remarque** : Il est recommandé d'activer ces tests pour renforcer la détection des spams. Cependant, certains tests peuvent entraîner des faux positifs ; ajustez en fonction de vos besoins.

---

## ⚙️ 3. Seuils de Marquage et de Suppression

- **Spam mark threshold** : Score à partir duquel un message est marqué comme spam (par défaut : `5`).
- **Spam delete threshold** : Score à partir duquel un message est supprimé sans être livré (par défaut : `20`).

> 📝 **Conseil** : Adaptez ces seuils en fonction de la sensibilité souhaitée. Un seuil de marquage plus bas augmente la détection, mais peut aussi accroître les faux positifs.

---

## ✉️ 4. Modification de l'Objet des Messages Spam

- **Add X-hMailServer-Spam header** : Ajoute un en-tête indiquant le score de spam.
- **Add X-hMailServer-Reason header** : Fournit la raison pour laquelle le message a été considéré comme spam.
- **Add to message subject** : Préfixe l'objet du message avec un texte spécifique (ex. : `[SPAM]`).

> 📌 **Astuce** : Ces options facilitent le tri des messages spam dans les clients de messagerie.

---

## 🧪 5. Intégration avec SpamAssassin

hMailServer peut s'intégrer à SpamAssassin pour une analyse approfondie des messages :

1. Activez l'option **Use SpamAssassin**.
2. Spécifiez l'**hôte** (par défaut : `localhost`) et le **port** (par défaut : `783`).
3. Cliquez sur **Test** pour vérifier la connexion.

> ⚠️ **Important** : Assurez-vous que le service SpamAssassin (spamd) est en cours d'exécution sur le serveur spécifié.

---

## 🗂️ 6. Configuration des Listes Noires DNS (DNSBL)

1. Accédez à :  
   `Settings > Anti-spam > DNS blacklists`
2. Cliquez sur **Add** pour ajouter une nouvelle liste noire.
3. Fournissez :
   - **DNS Host** : Nom de la liste (ex. : `zen.spamhaus.org`).
   - **Expected result** : Résultat attendu (souvent `127.0.0.2`).
   - **Reject message** : Message à retourner si le test est positif.
   - **Score** : Score à attribuer si le test est positif.

> 🔍 **Exemple** :  
> DNS Host : `zen.spamhaus.org`  
> Expected result : `127.0.0.2`  
> Reject message : `Rejected by Spamhaus`  
> Score : `5`

---

## 📄 7. Configuration des Listes Noires SURBL

1. Accédez à :  
   `Settings > Anti-spam > SURBL servers`
2. Cliquez sur **Add** pour ajouter une nouvelle liste.
3. Fournissez :
   - **DNS Host** : Nom de la liste (ex. : `multi.surbl.org`).
   - **Expected result** : Résultat attendu (souvent `127.0.0.2`).
   - **Reject message** : Message à retourner si le test est positif.
   - **Score** : Score à attribuer si le test est positif.

> 📝 **Remarque** : Les listes SURBL analysent les liens contenus dans les messages pour détecter des domaines associés au spam.

---

## ✅ 8. Configuration de la Liste Blanche

Pour éviter que des expéditeurs légitimes soient marqués comme spam :

1. Accédez à :  
   `Settings > Anti-spam > White listing`
2. Cliquez sur **Add**.
3. Spécifiez :
   - **Lower IP** et **Upper IP** : Plage d'adresses IP à autoriser.
   - **Email address** : Adresse email ou domaine à autoriser.
   - **Description** : Commentaire optionnel.

> 🔐 **Conseil** : Utilisez la liste blanche avec parcimonie pour ne pas compromettre l'efficacité des filtres anti-spam.

---

## 🧰 9. Autres Options

- **Maximum message size to scan** : Taille maximale des messages à analyser (en Ko).
- **Bypass spam checks for authenticated users** : Ignore les tests anti-spam pour les utilisateurs authentifiés.
- **Bypass spam checks for local to local email** : Ignore les tests pour les emails internes.

> ⚙️ **Astuce** : Ces options permettent d'optimiser les performances et d'éviter des analyses inutiles.

---

## 🔄 10. Test des Paramètres Anti-Spam

Pour vérifier l'efficacité de votre configuration :

1. Envoyez un email contenant la chaîne GTUBE suivante dans le corps du message :

   ```
   XJS*C4JDBQADN1.NSBN3*2IDNEN*GTUBE-STANDARD-ANTI-UBE-TEST-EMAIL*C.34X
   ```

2. Ce message doit être détecté comme spam par hMailServer.

> 🧪 **Remarque** : Ce test simule un message spam standard pour vérifier les filtres.

---

## 📚 Références

- Documentation officielle : [hMailServer Anti-Spam Reference](https://www.hmailserver.com/documentation/v5.6/?page=reference_antispam)
- Guide d'installation de SpamAssassin : [Charming Cloud Blog](https://charmingwebdesign.com/how-to-install-spamassassin-for-windows-and-spamd-service-hmailserver-forum/)

---


