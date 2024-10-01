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

![Capture d'écran des paramètres de date et heure](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Confg%C3%A9n%C3%A9raleFW.png)

---

## Configuration des interfaces réseau

Le Stormshield SN210 propose plusieurs interfaces réseau. Ci-dessous, nous décrivons la configuration de chaque interface :

### Interface `BRG_LAN`

Cette interface est utilisée pour le réseau interne protégé. Voici les étapes de configuration :

1. Sélectionnez l'interface **BRG_LAN** dans la liste des interfaces disponibles.
2. Assurez-vous que l'état de l'interface est activé (`ON`).
3. Paramètres généraux :
   - Nom de l'interface : `BRG_LAN`
   - Type d'interface : **Interne (protégée)**
4. Plan d'adressage :
   - Adresse IPv4 statique : `10.0.219.254/24`

### Interface `VLAN_MANA`

Cette interface est utilisée pour le réseau interne protégé. Voici les étapes de configuration :

1. Sélectionnez l'interface **VLAN_MANA** dans la liste des interfaces disponibles.
2. Assurez-vous que l'état de l'interface est activé (`ON`).
3. Paramètres généraux :
   - Nom de l'interface : `VLAN_MANA`
   - Type d'interface : **Interne (protégée)**
4. Plan d'adressage :
   - Adresse IPv4 statique : `192.168.0.126/24`


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

![Capture d'écran des interfaces réseau](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/interfacesFW.png)

---

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

![Capture d'écran conf finis ](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/administrationFW.png)

---

### Politique de Sécurité / Filtrage et NAT

Le firewall refuse par défaut notre connexion. Toutefois, si l'on modifie la politique de sécurité en la définissant sur **Pass All**, nous pourrons nous connecter.

1. Se rendre dans **Configuration** 
   - Sélectionner dans l'onglet **politique de Sécurité** la rubrique **Politique de Sécuriter / Filtrage et Nat**.

2. Sélectionner le niveau de **filtre**
   - Définir le niveau de filtre sur **(10) Pass ALL**

Voici une capture d'écran de la configuration :

![politiqueFW](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/politiqueFW.png)


