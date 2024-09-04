# Minicom

Minicom est un programme de communication serial pour accéder un équipement réseau ou sécurité par l'intermédiaire de son port console.
![Minicom](https://raw.githubusercontent.com/PatrickDummans/Bourges2025/main/images/Minicom.png)
Tout d'abord, il faut vérifier que toutes les mises à jour sont installées :
 ```sudo apt update```

Installons Minicom:
```sudo apt-get install minicom```

Vérifiez que vous avez des ports serial actifs:
```dmesg | grep tty```

Pour lancer le menu Minicom :
```sudo minicom -s```