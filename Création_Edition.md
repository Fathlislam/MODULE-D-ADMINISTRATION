# I - Fonctionnement 

## Informations générales
Résultat après l'ajout de profil ( voir : Listage de profiles), cette partie affiche le nom du profil ainsi que son numéro de profil.
Il est possible de supprimer totalement ce profil en cliquant sur la croix à gauche.  
 

## Droits sur les tables

A la création du profil,  (voir : Listage de profiles) nous arrivons sur la page de droit, on fait un select par rapport au profil (prf_id),
en fonction de cela on va afficher l'interface, 
et automatiquement cocher les enregistrements qui doivent être cocher. 
Il y a 3 colonnes en fonction de l'ajout, l’édition et suppression. 
Lorsqu'on va cocher une case, cela va déclencher un traitement Ajax qui va, dans un premier temps, vérifier l'état des 3 cases (s'il y a entrée ou non). 

Pour résumer, au clic sur l'une des croix, cela appellera une fonction Ajax qui a pour paramètre 
le nom de la table et le profile, si on a un enregistrement on fait un ``update`` de cet enregistrement,
sinon on fait un ``insert`` et on ajoute la table.

Le droit de lecture est le résultat des 3 colonnes (Ajout/Edition/suppression).
Pour ce droit on va faire un``select``, s'il y a une entrée, alors le droit de lecture est coché, 
mais s'il y a au moins l'une des 3 cases qui est cochée, alors la case (lecture) est cochée et grisée. 
Par contre, s'il n’y a pas d'entrée, on fait un ``insert`` et toutes ces valeurs seront à 0.

## Fonctionnalitées
`` En construction``


# II - En base de données

* *cli_profile_prf* :  Regroupe tout les profils. Les administrateurs clients de chaque site auront la possibilité de créer des profils avec des droits correspondants a leur attentes.  

* *cli_prf_ctb_jpc* :  jointure entre cli_profile_prf et cli_table_ctb.

* *cli_table_ctb* : elle regroupe la liste des tables avec les droits des administrateurs dessus. 

* *cli_sequence_sqc* :  Séquence utilisées pour les tables du schéma cli. 

