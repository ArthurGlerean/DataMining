Version de python: 3.13.2

Réflexions sur le système de recommandations:

Script de recommandations :
- **1ère étape:**
	- Récupérer l'ensemble des images (tags, couleurs) de tous les enregistrements utilisateur
		- tags_user = (*essemble de la liste des tags de chaque image*)
		- couleurs_user = (*essemble de la liste des couleurs de chaque image*)
		- infoscomplementaires_user = (*essemble de la liste des attriburs de chaque image*)
			- orientation (portrait, paysage)
			- taille (taille qui se rapproche +/- 10% de la taille qu'il a aimé en moyenne)
			- date => périodes qu'il a aimé => exclure celles qu'il n'a pas liké
- **2ème étape:**
	- Comparer chaque image et définir un niveau de similarité pour chaque:
		- Exemple, on passe sur une image:
			- On check les similitudes des tags avec les tags de l'utilisateur => Algorithme X
			- On check les similitudes des couleurs => Algorithme qui permet de révéler le rapprochement de couleurs => on établit un pourcentage global de ressemblance
			- Orientation : booléen
			- Algo pour déterminer l'écart de taille entre les deux valeurs de taille d'image (moyenne de taille d'image liké VS la taille de l'image comparée )
			- Date: on check si proche +/- 50 ans
			- => On se retrouve avec 5 pourcentages:
				- => On peut en faire une moyenne:
					- Si > 60% => on considère l'image comme similaire aux préférences de l'utilisateur
					- Sinon on ne la considère pas
					- Si on obtient aucune image => on réduit de -10% en -10% la condition (50%, puis s'il n'y a toujours rien 40%, etc.)
- **3ème étape**:
	- A cette étape, on a une liste d'images qui possède chacune un pourcentage de similarité
	- On propose à l'utilisateur celles avec le plus grand pourcentage, jusqu'aux plus petites