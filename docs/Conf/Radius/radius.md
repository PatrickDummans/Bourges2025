# 📡 Configuration d'une borne Wi-Fi Aruba avec authentification RADIUS

Ce guide détaille la configuration d'une borne Wi-Fi Aruba avec authentification RADIUS sur un serveur NPS (Network Policy Server). L'ordre des captures d'écran permet d'illustrer chaque étape de la configuration.

---

## 1️⃣ Réservation de l'adresse IP pour la borne Aruba
📌 **Objectif** : S'assurer que la borne Wi-Fi Aruba obtient toujours la même adresse IP via DHCP.

- Accédez à la **console DHCP**.
- Ajoutez une réservation avec :
  - **Adresse MAC** de la borne.
  - **Adresse IP** à attribuer.
  - **Description** : Borne Aruba.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Reservation%20Borne.PNG)

---

## 2️⃣ Ajout du client NPS pour l'authentification RADIUS
📌 **Objectif** : Déclarer la borne Aruba comme un client RADIUS sur le serveur NPS.

- Ouvrir la **console NPS**.
- Accéder à **Clients RADIUS**.
- Ajouter un nouveau client :
  - **Nom convivial** : `brg_aruba`
  - **Adresse IP** : `172.28.64.200`
  - **Fabricant** : RADIUS Standard
  - **État** : Activé
  - **Secret partagé** : Définir manuellement ou générer.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Client%20NPS.PNG) 
![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Conf%20Radius.PNG)

---

## 3️⃣ Configuration des contraintes d’authentification
📌 **Objectif** : Définir les méthodes d’authentification acceptées par le serveur NPS.

- Accédez à la stratégie réseau de VLAN sur NPS.
- Dans l'onglet **Contraintes**, configurer :
  - **Méthodes d’authentification** : Activer PEAP (Protected EAP).
  - **Désactiver** les méthodes non sécurisées comme PAP, CHAP.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Contraintes.PNG)

---

## 4️⃣ Configuration des conditions pour l'accès Wi-Fi
📌 **Objectif** : Autoriser uniquement les connexions Wi-Fi.

- Ouvrir les propriétés de la **stratégie réseau**.
- Dans l'onglet **Conditions**, ajouter :
  - **Type de port NAS** : Sans fil - IEEE 802.11.
  - **Groupes d’utilisateurs** : LOCAL\WConditionnement.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/VLAN%20Conditionnement%20(conditions).PNG)

---

## 5️⃣ Définition des paramètres RADIUS pour le VLAN
📌 **Objectif** : Configurer l’assignation dynamique du VLAN via RADIUS.

- Dans l'onglet **Paramètres**, définir :
  - **Framed-Protocol** : PPP.
  - **Service-Type** : Framed.
  - **Tunnel-Medium-Type** : 802.
  - **Tunnel-Server-Auth-ID** : `217`.
  - **Tunnel-Type** : Virtual LANs (VLAN).

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Vlan%20Condtionnement%20(Parametres).PNG)

---

## 6️⃣ Configuration des stratégies réseau
📌 **Objectif** : Définir les stratégies de connexion.

- Vérifier que les règles d’accès sont bien définies :
  - Autorisation des utilisateurs appartenant aux groupes sélectionnés.
  - Assignation dynamique du VLAN via attributs RADIUS.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Strat%C3%A9gies%20R%C3%A9seau.PNG)

---

## 7️⃣ Vérification des échanges RADIUS
📌 **Objectif** : Vérifier que l’authentification RADIUS est bien en place.

- Effectuer une **capture de paquets** avec Wireshark sur le port UDP 1812.
- Vérifier la présence de requêtes et réponses **Access-Request / Access-Accept**.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Capture%20Radius%20Trame.PNG)

---

## 8️⃣ Vérification sur l'administration de la borne Aruba
📌 **Objectif** : S’assurer que la borne est bien enregistrée et opérationnelle.

- Vérifier l’état de la borne dans la **console Aruba**.
- Confirmer que la connexion au serveur RADIUS est fonctionnelle.
- Vérifier la présence des clients connectés.

![Voir capture d'écran](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/Administration%20Borne%20Wifi%20Aruba.png)

---

## ✅ Conclusion
En suivant ces étapes, la borne Wi-Fi Aruba est correctement intégrée avec l'authentification RADIUS via NPS. L'attribution dynamique des VLANs et la sécurisation des accès via PEAP sont mises en place avec succès.

