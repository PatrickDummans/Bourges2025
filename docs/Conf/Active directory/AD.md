# Documentation du Script PowerShell

## Description
Ce script PowerShell permet d'importer des utilisateurs depuis un fichier CSV et de les ajouter dans Active Directory (AD) dans des Unités Organisationnelles (OU) spécifiques en fonction de leur fonction.

---

## Prérequis

Avant d'exécuter ce script, assurez-vous :

- D'avoir un fichier CSV contenant les utilisateurs avec les colonnes suivantes : `Prenom`, `Nom`, `Fonction`.
- D'avoir les privilèges nécessaires pour créer des utilisateurs dans Active Directory.
- D'exécuter le script sur un environnement compatible avec Active Directory (module **Active Directory** installé).
- Que le fichier CSV utilise `;` comme délimiteur.

---

## Structure du Fichier CSV

Le fichier CSV doit être formaté comme suit :

```csv
Prenom;Nom;Fonction
Jean;Dupont;Chauffeur
Marie;Martin;Secretaire
Pierre;Durand;Chefequipe
```

- **Prenom** : Prénom de l'utilisateur.
- **Nom** : Nom de famille de l'utilisateur.
- **Fonction** : Rôle de l'utilisateur (à choisir parmi : *Chauffeur*, *Secretaire*, *Chefequipe*).

---

## Fonctionnement du Script

1. **Importation des données** : Le script importe les informations des utilisateurs à partir du fichier CSV.
2. **Génération des identifiants** : Chaque utilisateur se voit attribuer un identifiant (`SamAccountName`) basé sur son prénom et son nom.
3. **Choix de l'OU** : L'utilisateur est ajouté à une OU spécifique selon sa fonction :
    - Chauffeur : `OU=Chauffeur,OU=Transport,OU=Organisation`
    - Secretaire : `OU=Secretaire,OU=Transport,OU=Organisation`
    - Chefequipe : `OU=Chefequipe,OU=Transport,OU=Organisation`
    - Autres fonctions : **OU par défaut** `OU=Transport,OU=Organisation`
4. **Vérification de l'existence** : Le script vérifie si l'utilisateur existe déjà dans Active Directory.
5. **Création de l'utilisateur** : Si l'utilisateur n'existe pas, il est créé avec les informations suivantes :
    - Nom complet
    - Adresse e-mail
    - Fonction
    - Mot de passe initial : `P@ssw0rd123456!`
6. **Résultat** : Le script affiche des messages confirmant la création ou la présence des utilisateurs.

---

## Code du Script

```powershell
$CSVFile = "C:\scripts\Transport.csv"
$CSVData = Import-CSV -Path $CSVFile -Delimiter ";" -Encoding UTF8

Foreach($Utilisateur in $CSVData){

    # Récupération des informations utilisateurs depuis le fichier CSV
    $UtilisateurPrenom = $Utilisateur.Prenom
    $UtilisateurNom = $Utilisateur.Nom
    $UtilisateurLogin = ($UtilisateurPrenom).Substring(0,1) + "." + $UtilisateurNom
    $UtilisateurEmail = "$UtilisateurLogin@bourges.sportludique.fr"
    $UtilisateurMotDePasse = "P@ssw0rd123456!"
    $UtilisateurFonction = $Utilisateur.Fonction

    # Choix de l'OU selon la fonction
    Switch ($UtilisateurFonction) {
        "Chauffeur" { $OU = "OU=Chauffeur,OU=Transport,OU=Organisation,DC=lan,DC=bourges,DC=sportludique,DC=fr" }
        "Secretaire" { $OU = "OU=Secretaire,OU=Transport,OU=Organisation,DC=lan,DC=bourges,DC=sportludique,DC=fr" }
        "Chefequipe" { $OU = "OU=Chefequipe,OU=Transport,OU=Organisation,DC=lan,DC=bourges,DC=sportludique,DC=fr" }
        Default {
            Write-Warning "La fonction '$UtilisateurFonction' de l'utilisateur $UtilisateurNom n'a pas d'OU correspondante. Utilisation de l'OU par défaut."
            $OU = "OU=Transport,OU=Organisation,DC=lan,DC=bourges,DC=sportludique,DC=fr"
        }
    }

    # Vérifier la présence de l'utilisateur dans Active Directory
    if (Get-ADUser -Filter {SamAccountName -eq $UtilisateurLogin}) {
        Write-Warning "L'identifiant $UtilisateurLogin existe déjà dans l'AD"
    }
    else {
        # Création de l'utilisateur dans l'OU appropriée
        New-ADUser -Name "$UtilisateurNom $UtilisateurPrenom" `
                    -DisplayName "$UtilisateurNom $UtilisateurPrenom" `
                    -GivenName $UtilisateurPrenom `
                    -Surname $UtilisateurNom `
                    -SamAccountName $UtilisateurLogin `
                    -UserPrincipalName "$UtilisateurLogin@bourges.sportludique.fr" `
                    -EmailAddress $UtilisateurEmail `
                    -Title $UtilisateurFonction `
                    -Path $OU `
                    -AccountPassword (ConvertTo-SecureString $UtilisateurMotDePasse -AsPlainText -Force) `
                    -ChangePasswordAtLogon $true `
                    -Enabled $true

        Write-Output "Création de l'utilisateur : $UtilisateurLogin ($UtilisateurNom $UtilisateurPrenom) dans l'OU : $OU"
    }
}
```

---

## Exécution du Script

1. **Placez le fichier CSV** à l'emplacement `C:\scripts\Transport.csv`.
2. **Ouvrez PowerShell en tant qu'administrateur**.
3. **Exécutez le script** :
   ```powershell
   .\NomDuScript.ps1
   ```

---

## Messages de Sortie

- **Succès** : `Création de l'utilisateur : [Login] ([Nom] [Prenom]) dans l'OU : [OU]`
- **Avertissement** : `L'identifiant [Login] existe déjà dans l'AD` ou `La fonction '[Fonction]' de l'utilisateur [Nom] n'a pas d'OU correspondante.`

---

## Notes
- Le mot de passe initial est statique (`P@ssw0rd123456!`). Changez-le si nécessaire.
- Ajoutez d'autres fonctions dans le bloc `Switch` si besoin.
- Le code ci-dessus est un exemple d'un cas concret il faudra donc modifier certaines choses telle que le **csvfile** et les **OU**
---
