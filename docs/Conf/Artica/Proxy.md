# Proxy Artica 

**Artica Proxy** est une solution logicielle conçue pour la gestion des proxys et l'optimisation des réseaux d'entreprise. Elle offre une plateforme tout-en-un qui combine des fonctionnalités de proxy HTTP/HTTPS, de filtrage de contenu, de contrôle d'accès et de gestion de la bande passante.

---

## Filtrage / Bloquage de site internet.

**Doc artica** : https://www.artica-protect.fr/wp-content/uploads/2021/09/documentation-4.30.000000.pdf

Documentation qui n'est pas totalement a jours mais utilisable tout de même. 

### Installation de Artica 

Prérequis : - Image .iso de artica 
            - Virtualisation ( nutanix pour nous ) 

Lancer la VM et suivre l'assistant d'installation : 

- configurer l'ip 
- configurer la Gateway
- configurer le DNS (ip + nom de domaine)

Une foit la configuration faites ce connecter en entrant l'addresse ip qui nous ai donner en n'oubliant pas de vérifier que l'addresse est bien router et NATer.

Capture d'écran de la console
![console](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/console.png)

### Config Web 

- Apres avoir fait les config de base, mise a jours etc ...

- Ce rendre dans Service de filtrage / Fonctionalités  

- installer le service de filtrage et filtrage web

- mettre a jours les catégories

- ce rendre dans Blocage de site Web et ajouter les sites que vous essayez de bloquer. 

- veillez a utiliser le proxy artica et pas un autre (paramètre navigateur)

![filtrage](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/filtrage.png)
            
