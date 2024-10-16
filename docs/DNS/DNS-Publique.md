# Documentation de Configuration DNS sous Windows Server

## 1. Ouvrir le Gestionnaire DNS

### Capture d'écran :
![Gestionnaire DNS](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/DNS.png)

Le **Gestionnaire DNS** permet de gérer les zones DNS et d'administrer la résolution des noms dans un réseau. Dans cet exemple, deux zones de recherche directe sont configurées :
- **bourges.sportludique.fr** : Zone principale standard
- **lan.bourges.sportludique.fr** : Zone principale standard

L'état de ces zones est en cours d'exécution et DNSSEC n'est pas signé pour ces zones.

## 2. Détails de la zone `bourges.sportludique.fr`

### Capture d'écran :
![Détails Zone](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/DNS1.png)

Cette capture présente les enregistrements DNS pour la zone **bourges.sportludique.fr**. Voici les enregistrements configurés :
- **SOA (Start of Authority)** : Indique l'autorité principale pour la zone, ici le serveur `brg-winserv2019`.
- **NS (Name Server)** : Définit le serveur DNS autoritaire pour la zone, ici `brg-winserv2019`.
- **A (Host)** : L'enregistrement de type `A` associe le nom de domaine `www` à l'adresse IP `192.168.18.3`.

## 3. Gestion des rôles et fonctionnalités DNS

### Capture d'écran :
![Gestionnaire de Serveur](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/ConfigDNS.png)

Dans le **Gestionnaire de serveur**, vous pouvez ajouter ou supprimer des rôles et fonctionnalités, gérer des serveurs ou créer des groupes de serveurs. Pour configurer ou modifier les fonctionnalités DNS, suivez les étapes ci-dessous :
1. Cliquer sur **Gérer** dans le menu en haut à droite.
2. Sélectionner **Ajouter des rôles et fonctionnalités** pour ajouter le rôle DNS si ce n'est pas déjà fait.
3. Suivre les instructions de l'assistant pour ajouter le rôle DNS.

---

## Conclusion

Ce guide a présenté les principales étapes de la configuration DNS sur un serveur Windows, y compris l'ajout et la gestion des zones DNS, ainsi que la gestion des rôles via le Gestionnaire de serveur.

