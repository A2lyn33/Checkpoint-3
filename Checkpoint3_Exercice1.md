# 💪 Challenge
## **Exercice 1 : Manipulations pratiques sur VM Windows (temps estimé : 1h30)**
>Pour cet exercice tu as besoin de la VM SRVWIN01.

## Partie 1 : Gestion des utilisateurs
>L'utilisateur Kelly Rhameur a quitté l'entreprise.
>Elle est remplacée par Lionel Lemarchand

### Q.1.1.1 _Créer l'utilisateur Lionel Lemarchand avec les même attribut de société que Kelly Rhameur._
![Capture d’écran 2025-01-17 095213](https://github.com/user-attachments/assets/f00b244c-95ce-430d-9b66-4cd0b10b2609)
![Capture d’écran 2025-01-17 100951](https://github.com/user-attachments/assets/71e29e07-2365-40b6-9b8f-11b2fddd73c4)
![Capture d’écran 2025-01-27 113314](https://github.com/user-attachments/assets/15cb8ea8-edbb-4de0-b18d-71bfaa58e6d6)


### Q.1.1.2 _Créer une OU DeactivatedUsers et déplace le compte désactivé de Kelly Rhameur dedans._
![Capture d’écran 2025-01-17 102827](https://github.com/user-attachments/assets/74d823a9-8612-49be-b688-345b67eced85)
![Capture d’écran 2025-01-27 113502](https://github.com/user-attachments/assets/67d5bcd8-4643-4a6a-bcf6-ae3e714786af)
![Capture d’écran 2025-01-17 102840](https://github.com/user-attachments/assets/0b95d3e0-5b70-4624-9a51-13ec51a20b9e)
![Capture d’écran 2025-01-17 102917](https://github.com/user-attachments/assets/167c2f19-15bc-43d3-90db-249fecb5fa3c)

### Q.1.1.3 _Modifier le groupe de l'OU dans laquelle était Kelly Rhameur en conséquence._
![Capture d’écran 2025-01-17 103124](https://github.com/user-attachments/assets/522f9649-7a4d-4bd6-8cf5-fbccda6e6842)

### Q.1.1.4 _Créer le dossier Individuel du nouvel utilisateur et archive celui de Kelly Rhameur en le suffixant par -ARCHIVE._
![Capture d’écran 2025-01-17 103543](https://github.com/user-attachments/assets/6e61dbd1-a035-40d5-bd5f-27f82c9ec8fb)

---
## Partie 2 : Restriction utilisateurs

### Q.1.2.1 _Faire en sorte que l'utilisateur Gabriel Ghul ne puisse se connecter que du lundi au vendredi, de 7h à 17h._
![Capture d’écran 2025-01-17 110659](https://github.com/user-attachments/assets/4b76a1f2-c0e7-4982-9252-625e3dcb373c)

### Q.1.2.2 _De même, bloquer sa connexion au seul ordinateur CLIENT01._
![Capture d’écran 2025-01-17 110914](https://github.com/user-attachments/assets/2501a5d8-5efd-4e5a-8225-c7ae5dd52720)

### Q.1.2.3 _Mettre en place une stratégie de mot de passe pour durcir les comptes des utilisateurs de l'OU LabUsers._
![Capture d’écran 2025-01-17 112252](https://github.com/user-attachments/assets/031d1494-dbdf-40a1-bf03-da922eaf1d01)

---

## Partie 3 : Lecteurs réseaux

### Q.1.3.1 _Créer une GPO Drive-Mount qui monte les lecteurs E: et F: sur les clients._
![Capture d’écran 2025-01-17 113828](https://github.com/user-attachments/assets/d580bb3e-9385-4e11-bf24-b693f5b22b2b)
![Capture d’écran 2025-01-17 114402](https://github.com/user-attachments/assets/e4cc0b40-cdbb-48b9-8650-f944937cf3e4)
![Capture d’écran 2025-01-17 114606](https://github.com/user-attachments/assets/eb7320e7-00b9-4cb6-be19-6e92045961d5)
![Capture d’écran 2025-02-02 160506](https://github.com/user-attachments/assets/e40ac162-5aed-4a93-ad4a-31ea0033a46c)
![Capture d’écran 2025-02-02 160534](https://github.com/user-attachments/assets/041036c5-e272-4871-970d-3613e2e914d3)
![Capture d’écran 2025-02-02 160557](https://github.com/user-attachments/assets/c4ce4433-d3f9-4ed5-b9c0-41e0365aed40)
![Capture d’écran 2025-02-02 160635](https://github.com/user-attachments/assets/e49cf33c-f7f9-4199-a160-39783bc76b92)


