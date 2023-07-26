## Introduction à MongoDB

Utilisation de la sandbox en ligne [disponible ici](https://www.humongous.io/app/playground/mongodb/new)

Utiliser le [jeu de données suivant](https://raw.githubusercontent.com/vincent2mots/bga/main/NOSQL/Documents/sample_movies.bson)

Introduire le jeu de données dans l'onglet **"Database content"** et exécuter les requêtes suivantes.

### Quelques exemples de requêtes à passer :
Chercher un élément dans la collection :
```
db.collection.findOne()
```

Compter le nombre de documents dans la collection : 
```
db.movies.count()
```

Chercher tous les documents dont le film est de type **Action** :
```
db.collection.find({
    "genres": "Action"
})
```

Compter le nombre de films est de type **Action** :
```
db.collection.count({
    "genres": "Action"
})
```