# I - Fonctionnement 

## Liste des profiles

Cette action permet l'affichage de la liste des profiles correspondant au site géographique sélectionné au préalable après la connexion. Ce cas va récupérer la liste des profiles enregistrés dans la table `cli_profile_prf` dans le fichier `prf.class.php` ainsi que les restrictions. Les restrictions permettront de donner le droit à la suppression de profil ou non, Si un profil n'a pas de restriction ( restriction = 1), il peut supprimer un profil sans être supprimer par un autre. par contre si la restriction est à 0, il n'aura pas le droit de supprimer de profil.  
 

## Ajouter profil
Correspond au cas `createPrf `, qui sera appeler lorsque l'on clique sur l'icone ( + ) et traité dans la fonction d'édition de profil (prfedit). 
Cela permet d’accéder à un formulaire où il est demandé de renseigner un nom de profil puis d'enregistrer les modifications en cliquant sur créer le profil .
Après cela, l'utilisateur est dirigé vers l'interface de création et édition ( voir : Création et Edition/ Informations générales).


## Affichage du détail du profil

Cette partie permet l’accès aux droits du profil sur les tables.  (voir : Création et Edition) 


# II - En base de données

* *cli_profile_prf* :  Regroupe tout les profils. Les administrateurs clients de chaque site auront la possibilité de créer des profils avec des droits correspondants a leur attentes.  

* *cli_site_sit* :  Liste des sites géographiques du client.
