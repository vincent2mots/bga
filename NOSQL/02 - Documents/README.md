## Introduction à MongoDB

Utilisation de la sandbox en ligne [disponible ici](https://www.humongous.io/app/playground/mongodb/new)

Utiliser le [jeu de données suivant](https://raw.githubusercontent.com/vincent2mots/bga/main/NOSQL/Documents/sample_movies.bson)

Introduire le jeu de données dans l'onglet **"Database content"** et exécuter les requêtes suivantes.

### Quelques exemples de requêtes à passer :
Chercher un élément dans la collection :
```
db.collection.findOne()
```
Ici, aucun paramètre n'est renseigné dans la fonction findOne(). En conséquence, c'est le premier document qu'il trouve qui est retourné.

Compter le nombre de documents dans la collection : 
```
db.collection.count()
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

Trouver les films dont le titre contient **1995** :
```
db.collection.find({"title" : /.*1995.*/})
```

### Insertion de donnée
Insertion d'un nouveau film dans la collection :
```
db.collection.insertOne(
    { "_id" : 139, "title" : "Oppenheimer (2023)", "genres" : ["Drama", "Biopic"], "year": 2023 }
)
```

Au passage, notez qu'il n'est pas nécessaire que le nouveau document ait exactement la même structure que les autres. Ici, il possède le champ "year" que les autres n'ont pas.

### Modification d'un document
Modifier le titre d'un document :
```
db.collection.update(
    { _id: 1},
    {
        $set: {
            title: "Toy Story (1995), super film"
        }
    }
)
```

**Attention** : cette instruction ne fonctionne pas sur cet environnement de démonstration.