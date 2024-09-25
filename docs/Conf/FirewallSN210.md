# Documentation de configuration du pare-feu Stormshield SN210

## Table des matières
1. [Configuration de la date et de l'heure](#configuration-de-la-date-et-de-lheure)
2. [Configuration des interfaces réseau](#configuration-des-interfaces-réseau)
   - [Interface `in`](#interface-in)
   - [Interface `out`](#interface-out)
   - [Interface `dmz1`](#interface-dmz1)

---

## Configuration de la date et de l'heure

Pour configurer les paramètres de date et d'heure sur le Stormshield SN210, voici les étapes à suivre :

1. Allez dans le menu **Paramètres de date et d'heure**.
2. Vous pouvez choisir de :
   - Saisir l'heure manuellement
   - Synchroniser l'heure avec la machine
   - Maintenir le firewall à l'heure via un serveur NTP (recommandé).

### Exemple de configuration

Voici un exemple de configuration avec deux serveurs NTP utilisés pour synchroniser l'horloge du pare-feu :
- `ntp1.stormshielddcs.eu`
- `ntp2.stormshielddcs.eu`

Fuseau horaire configuré : `Europe/Paris`.

![Capture d'écran des paramètres de date et heure](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/ddd.png)

---

## Configuration des interfaces réseau

Le Stormshield SN210 propose plusieurs interfaces réseau. Ci-dessous, nous décrivons la configuration de chaque interface :

### Interface `in`

Cette interface est utilisée pour le réseau interne protégé. Voici les étapes de configuration :

1. Sélectionnez l'interface **in** dans la liste des interfaces disponibles.
2. Assurez-vous que l'état de l'interface est activé (`ON`).
3. Paramètres généraux :
   - Nom de l'interface : `in`
   - Type d'interface : **Interne (protégée)**
4. Plan d'adressage :
   - Adresse IPv4 statique : `192.168.255.126/25`

Voici une capture d'écran de cette configuration :

![Capture d'écran de l'interface in](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/fff.png)

### Interface `out`

L'interface `out` est généralement utilisée pour la connexion à Internet. Pour configurer cette interface :

1. Sélectionnez l'interface **out**.
2. Vérifiez que l'état est activé.
3. Paramètres généraux :
   - Nom de l'interface : `out`
   - Type : Ethernet
4. Plan d'adressage :
   - Adresse IPv4 : à configurer selon votre réseau.

### Interface `dmz1`

L'interface `dmz1` est utilisée pour les zones démilitarisées (DMZ). Cette zone est utilisée pour héberger des services accessibles depuis l'extérieur tout en isolant le reste du réseau interne.

1. Sélectionnez l'interface **dmz1**.
2. Paramètres généraux :
   - Nom de l'interface : `dmz1`
   - Type d'interface : Ethernet
3. Plan d'adressage :
   - Adresse IPv4 : `192.168.18.1/24`.

Voici une capture d'écran de la configuration des interfaces :

![Capture d'écran des interfaces réseau](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/fff.png)


### Accès aux pages d'administration du firewall

Dans notre cas, il est indispensable de pouvoir accéder au firewall depuis le VLAN de management. Nous allons donc ajouter un accès aux pages d'administration du firewall.

1. Se rendre dans **Configuration** :
   - Sélectionner dans l'onglet **Système** la rubrique **Configuration**.
   - Sélectionner **Administration du Firewall**.

2. Se rendre dans la partie **"Accès aux pages d'administration du firewall"** :
   - Cliquer sur le petit **+ Ajouter** en haut à gauche de l'interface.
   - Choisir **Réseaux** à gauche.
   - Remplir les champs **Nom** et **Réseau**.

Voici des captures d'écran de la configuration :


![Capture d'écran pas finis](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/confobjet.png)

![Capture d'écran conf finis ](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/sss.png)
