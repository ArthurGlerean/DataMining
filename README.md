Version de python: 3.13.2

Donc solution pour les doublons d'images:

- Premier appel qui récupère juste les images sans informations complémentaires
    - J'ai déjà ajoutée cette requete dans la fonction qui download les images
- Ensuite, a partir des images récupérées (qui ont toute un QXXXXXX) faire la requete suivante pour récupérer les informations complémentaires:
    ```sql
    SELECT ?item ?title ?artistLabel ?year ?movementLabel 
           ?materialLabel ?locationLabel ?depictsLabel ?countryLabel ?pic{

  VALUES ?item {wd:Q609576 wd:Q609572}
      #OPTIONAL { ?item wdt:P1476 ?title. }         # Titre
      OPTIONAL { ?item wdt:P170 ?artist. }         # Artiste
      OPTIONAL { ?item wdt:P571 ?date. }           # Date de création
#       OPTIONAL { ?item wdt:P31 ?type. }            # Type d'œuvre
      OPTIONAL { ?item wdt:P135 ?movement. }       # Mouvement artistique
      OPTIONAL { ?item wdt:P186 ?material. }       # Matériau utilisé
      OPTIONAL { ?item wdt:P276 ?location. }       # Lieu de conservation
      OPTIONAL { ?item wdt:P180 ?depicts. }        # Sujet représenté
      OPTIONAL { ?item wdt:P495 ?country. }        # Pays d’origine
             
                   # Extraction de l'année seulement
      BIND(YEAR(?date) AS ?year)

      SERVICE wikibase:label { bd:serviceParam wikibase:language "fr,en". }
}
LIMIT 1
    ```

**ATTENTION**: bien penser lors de la premiere requete à stocker le QXXXXXX pour pouvoir le réutiliser dans la deuxieme query.