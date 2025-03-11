# Documentation : Installation de Wazuh et de ses agents

## 1. Introduction
Wazuh est une plateforme open-source pour la détection des menaces, la surveillance de l'intégrité des fichiers et la gestion des logs. Cette documentation détaille l'installation du serveur Wazuh et l'ajout d'un agent.

---

## 2. Installation du Serveur Wazuh
### 2.1 Prérequis
- Système d'exploitation : **Ubuntu 20.04 / 22.04** ou **CentOS 7/8**
- **Accès root**
- **2 Go de RAM minimum** (8 Go recommandés pour production)
- **10 Go d’espace disque minimum**

### 2.2 Installation du Serveur Wazuh
#### 2.2.1 Ajouter le dépôt Wazuh
```bash
curl -sO https://packages.wazuh.com/4.11/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

#### 2.2.2 Accéder à l’interface Web
Ouvrir un navigateur et accéder à :
```
http://<IP_SERVEUR>:(leportindiqué)
```

## 3. Installation des clients


![1eretape](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/1eretape.png)

![2emeetape](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/2emeetape.png)

![3emeetape](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/refs/heads/main/images/3emeetape.png)

