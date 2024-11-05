## Serveur DHCP sous windows

Les actions réalisées ont été effectuées sur des machines virtuelles avec un poste serveur (Windows serveur 2022) et un poste client ( Windows 10 Famille)

### Installation du serveur

<HR>

Il faut en premier lieu configurer nos VMs : 

| | Serveur | Client
| :-: | :-: | :-: |
| Nom | SRV-WIN-DHCP | NomUser|
| Adresse IP | Statique : 172.20.0.1 | Automatique (DHCP) |
| Carte réseau | Réseau interne | Réseau interne |

<HR>

Passons au serveur, il faut lui ajouter le rôle DHCP.
<HR>
- Dans le gestionnaire de serveur, sélectionnez *Gérer* puis *Ajouter des rôles et fonctionnalités*


![role](https://i.imgur.com/PWQLxDB.png)
<HR>

- Choisissez *Installation base sur un rôle ou une fonctionnalité* puis *suivant*

![insta](https://i.imgur.com/IG3WzzD.png)
<HR>

- Le serveur est déjà sélectionné, *suivant*

![selec](https://i.imgur.com/g7Eund6.png)
<HR>

- Sélectionnez __Serveur DHCP__ puis *suivant* (Confirmer avec *ajouter des fonctionnalités* pour la pop-up qui est apparu)

![dhcp](https://i.imgur.com/2hXzbHI.png)
<HR>

- *Suivant* jusqu'à la confirmation pour appuyer sur *Installer*


##### Il faut maintenant redémarrer le PC.
<HR>

### Création d'une étendue DHCP

<HR>

- Dans les outils, ouvrez la *"console DHCP"*

![console](https://i.imgur.com/ue9Kdw2.png)
<HR>

- Vous arrivez dans un interface de ce style :

![cons](https://i.imgur.com/W0Eun6Q.png)
<HR>

- Clique droit sur *IPv4* puis -> *Nouvelle étendue*. Une fenêtre d'assistance apparaît.

![assist](https://i.imgur.com/W0Eun6Q.png)
<HR>

- Indiquez le nom de l'étendue puis *suivant*

![nomrange](https://i.imgur.com/LZrcSKm.png)
<HR>

- __La partie la plus importante. Ici il faut renseigner la plage IP de l'étendue, c'est à dire les adresses que le serveur DHCP pourra distribuer aux clients qui se présente à lui.__

  > Pour rappel, l'adresse IP du serveur est 172.20.0.1. Il faut donc une place sur la même base réseau.
  > Prenons comme plage 172.20.0.100 à 172.20.0.200 sans oublier le CIDR à 24.


![plageip](https://i.imgur.com/QiUMLUu.png)
<HR>

- Si vous voulez exclure des plages afin qu'elle ne soit pas distribuées par le serveur, vous pouvez renseigner une plage d'ip à ne pas distribuer. Pensez à les *Ajouter*.

 > Ici, nous n'en avons pas de besoin.

![exclure](https://i.imgur.com/5CbtfDe.png)
<HR>

- Pour la durée du bail, elle est par défaut à 8 jours. Nous allons la laissé telle qu'elle.

![bail}(https://i.imgur.com/H5LUBdO.png)
<HR>

- Pour l'ajout de routeur, passerelle ou autre fonction, cochez oui, sinon vous pourrez les configurer plus tard. Dans notre cas non n'en avons pas besoin.

![rout](https://i.imgur.com/irspY62.png)
<HR>

- Voici la fin de la création de l'étendue. Pensez à l'activer. Terminez l'action en appuyant sur *Terminer*
<HR>

- Vous devriez avoir une console resemblant à ceci :


![console2](https://i.imgur.com/55TYl7h.png)

### Sur le poste client

En lançant le client, le serveur DHCP devrait lui attribuer une adresse IP compris dans la plage de notre étendue. Vérifions ça à l'aide de ```ipconfig /all ``` dans la console.

- Voici un aperçu :

![ipconfig](https://i.imgur.com/UOM1cxv.png)
<HR>
