# 🔁 Mise en place de HSRP pour la haute disponibilité sur le VLAN 213

## 🧩 Objectif
Assurer la **haute disponibilité réseau** sur le **VLAN 213 (192.168.255.0/25)** en configurant le protocole **HSRP** (Hot Standby Router Protocol) entre deux routeurs : **BRG-R2 (principal)** et **BRG-R1 (secondaire)**.

---

## 🔧 1. Prérequis

- **Réseau concerné** : `192.168.255.0/25`
- **Adresse IP virtuelle HSRP** : `192.168.255.254`
- **Encapsulation** : `dot1Q` sur le VLAN 213
- **Interfaces utilisées** : `GigabitEthernet0/1.212` (sous-interface pour le VLAN 213)
- **HSRP Group** : `10`
- **Preempt activé** sur les deux routeurs
- **Passerelle par défaut des hôtes** : `192.168.255.254`

---

## 📍 2. Configuration du Routeur Principal : `BRG-R2`

### 🔹 Informations
- **Interface** : `GigabitEthernet0/1.212`
- **IP réelle** : `192.168.255.252/25`
- **Priorité HSRP** : `110` (supérieure au secondaire)
- **Preempt** : Activé ✅

### ⚙️ Configuration
```bash
interface GigabitEthernet0/1.212
 encapsulation dot1Q 213
 ip address 192.168.255.252 255.255.255.128
 standby 10 ip 192.168.255.254
 standby 10 priority 110
 standby 10 preempt
```

---

## 📍 3. Configuration du Routeur Secondaire : `BRG-R1`

### 🔹 Informations
- **Interface** : `GigabitEthernet0/1.212`
- **IP réelle** : `192.168.255.253/25`
- **Priorité HSRP** : `100` (par défaut)
- **Preempt** : Activé ✅

### ⚙️ Configuration
```bash
interface GigabitEthernet0/1.212
 encapsulation dot1Q 213
 ip address 192.168.255.253 255.255.255.128
 standby 10 ip 192.168.255.254
 standby 10 preempt
```

---

## 🧠 4. Bonnes pratiques et rappels HSRP

- Les deux routeurs doivent :
  - Être dans le **même sous-réseau**
  - Partager la **même IP virtuelle HSRP**
  - Avoir le **même numéro de groupe** (ex: `10`)
- Le **routeur avec la priorité la plus élevée devient actif**
- Le **preempt** permet à un routeur redevenu disponible de reprendre le rôle actif s’il a une priorité plus élevée
- La **gateway par défaut** des hôtes du VLAN 213 doit être : `192.168.255.254`

---

## ✅ 5. Vérifications après déploiement

- 🔎 **Vérifier l’état HSRP** :
```bash
show standby
```

- ✅ **Vérifier l’activation de dot1Q** sur les interfaces :
  - La commande `show running-config interface GigabitEthernet0/1.212` doit afficher `encapsulation dot1Q 213`

- 🧪 **Tester le basculement HSRP** :
  - Éteindre brièvement le routeur principal et s'assurer que le secondaire prend le relais
  - Puis rallumer le principal et vérifier qu’il redevient actif grâce au `preempt`

- 💡 **Sur les hôtes du VLAN 213** :
  - S’assurer que leur **passerelle** est bien `192.168.255.254` (pas l’IP réelle d’un routeur)

---

