# I - Fonctionnement

## Liste des tables

C'est le cas appelé par défaut lorsqu'on clique sur le module de gestion des tables dans le menu : l'affichage de la liste des tables. L'affichage de la liste des tables va varier en fonction du profil administrateur qui se connecte. Ce cas va récupérer la liste des tables enregistrés dans la table *cli_table_ctb* dans le fichier **table.class.php**. Cependant pour gérer l’accès à une table il y a un champ qui indique le niveau d'administration minimum à avoir afin de pour réaliser des actions. Une condition est donc nécessaire pour vérifier si l’utilisateur connecté a accès ou non à la table. 
`if($_SESSION['prf_id']<=$table['level_admin'])`
 Ensuite la liste de tables accessible est affiché sous forme de lien et ces liens redirigent vers un autre cas afin de consulter le contenu de la table dans le fichier **table.html.php**. 
`echo "<li  class=\"list-group-item\"><a href='#' id=".$i." onclick=\"jsGlobalCRequestT('html','adm','table','afficherTable','','',".$arrArgument.");\"  >".$table['ctb_lib']."</a></li>"; `
Ce code va permettre de réalisé un appel vers le même module mais pour le cas *afficherTable* mais avec le nom de la table à afficher. 

## Affichage du contenu d'une table

 Ce cas correspond au cas *afficherTable*. Ce cas va être appeler lorsque l'on clique sur un des liens présents dans la listes des tables. Il permet d'afficher le contenu de la table.
Dans un premier temps c'est dans li fichier **table.class.php** que l'on va récupérer le contenu de la table reçu en paramètre. Ensuite je récupère les informations de la tables ( contraintes, clés étrangère...). Pour l'affichage dans le fichier **table.html.php**, on va afficher la description de la table. Pour les champs d'affichage du tableau, on va récupérer dans la table  *sys_database_object_sdo* la description de ce champ à l'aide de 4 paramètres (qui représentent la clé primaire) : le nom du champ, type de l'objet (field, table...), le code du schéma (sys ou cli) et le trigramme de la table. On vérifie si le champ récupérer est une clés étrangère, si s'en est une on fait le même procédé avec le champ référence récupéré dans la requêtes précédente (lui aussi stocké), sinon on l'affiche la description récupéré.
  Ensuite pour le contenu de la table, on va parcourir la liste des valeurs en parallèle avec la liste des informations sur la table. On vérifie s'il existe des contraintes sur le champ courant, si c'est une clé étrangère, on va récupéré la valeur de cette clés et l'afficher (pour que ce soit plus parlant pour l'utilisateur). Si c'est une clé primaire, on va générer des icone pour la suppression et l'édition. S'il n'y a pas de contraintes on affiche le champ tout simplement. Et voila on a l'affichage du contenu de la table.

## Edition d'une ligne

Pour l'édition d'une ligne, il faut cliquer sur le bouton d'édition et un modal va apparaître. Le modal vide est enregistrée dans le fichier **table.html.php** et est complété à l'aide d'un appel ajax. Cet appel ajax est réalise au moment de cliquer sur le bouton editer. Il va envoyer en paramètre la clés primaire de la table, sa valeur, le schéma correspondant, ainsi que la table concerné. Avec ces information , un formulaire pré remplie est créer dans le fichier **table.ajax.php**, après récupération des informations dans le **table.class.php**. L'affichage du formulaire va varier en fonction du type de champ : si c'est une clés étrangère on aura un select qui va nous permettre de choisir la valeur souhaitée. Sinon c'est un champ texte tout simplement avec la valur correspondante, qui peut être obligatoire. 
Lorsque l'utilisateur apporte ses modifications, les valeurs sont récupérés en javascript et envoyé vers un cas qui va s'occuper du traitement. C'est le cas *updatesql*. Ce cas s’exécute dans le fichier **table.class.php** en passant par le fichier ajax et va générer et exécuter une requêtes de mis à jour. 

## Ajout d'une ligne

Pour l'ajout d'une ligne, c'est pratiquement le même procédé que lors de l'édition mis à part que c'est une requêtes d'insertion à la fin, et que le formulaire ne sera pas pré remplie. . 

## Suppression d'une ligne

La suppression d'une ligne se fait en cliquant sur le bouton de suppression. Celui ci va envoyer 4 paramètres : la clés primaire de la table, sa valeur pour la ligne choisis, le schéma correspondant, ainsi que la table concerné. Cela va ensuite afficher un modal de confirmation, si on clique sur le bouton oui, on réalise un appel ajax qui correspond au cas *dropLigne*. Ce cas va appeler le fichier class qui va générer une requête de suppression et l’exécuter pour la ligne demandée.

# II - En base de données

En base de données deux tables sont utilisés essentiellement cependant aucune modification ne leur est apportés : 

* *cli_table_ctb* : elle regroupe la liste des tables avec les droits des administrateurs dessus. 
* *sys_database_object_sdo* : elle contient tout les champs et tables du schéma ainsi que les contraintes. 
