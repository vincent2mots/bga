## Test d'utilisation d'une base de données NOSQL de type Graphes
Pour cet exercice, utilisation de la sandbox Neo4J (Bac à sable), disponible ici gratuitement : [cliquer ici](https://sandbox.neo4j.com/)

Se créer un compte à l'aide de Google par exemple.

Le bac à sable Neo4j propose plusieurs datasets. Utiliser le projet "Movies" pour l'exercice suivant.

### **Find** : pour trouver des noeuds individuels
Trouver un acteur qui s'appelle "Tom Hanks" : 
```
MATCH (tom {name: "Tom Hanks"}) RETURN tom
```

Trouver un film dont le titre est "Cloud Atlas" : 
```
MATCH (cloudAtlas {title: "Cloud Atlas"}) RETURN cloudAtlas
```

Trouver 10 personnes :
```
MATCH (people:Person) RETURN people.name LIMIT 10
```

Trouver des films sortis dans les années 1990 :
```
MATCH (nineties:Movie) WHERE nineties.released >= 1990 AND nineties.released < 2000 RETURN nineties.title
```

### **Query** : pour trouver des modèles (pattern) dans la donnée
Lister tous les films de Tom Hanks :
```
MATCH (tom:Person {name: "Tom Hanks"})-[:ACTED_IN]->(tomHanksMovies) RETURN tom,tomHanksMovies
```

Qui a réalisé le film "Cloud Atlas"?
```
MATCH (cloudAtlas {title: "Cloud Atlas"})<-[:DIRECTED]-(directors) RETURN directors.name
```

Lister les co-acteurs de Tom Hanks : 
```
MATCH (tom:Person {name:"Tom Hanks"})-[:ACTED_IN]->(m)<-[:ACTED_IN]-(coActors) RETURN coActors.name
```

Trouver les personnes qui sont associées au film "Cloud Atlas" :
```
MATCH (people:Person)-[relatedTo]-(:Movie {title: "Cloud Atlas"}) RETURN people.name, Type(relatedTo), relatedTo
```

### **Solve** : pour résoudre
Les films et les acteurs qui sont à "6 sauts" de Kévin Bacon : 
```
MATCH (bacon:Person {name:"Kevin Bacon"})-[*1..4]-(hollywood)
RETURN DISTINCT hollywood
```

Le chemin le plus court entre Kévin Bacon et Meg Ryan : 
```
MATCH p=shortestPath(
(bacon:Person {name:"Kevin Bacon"})-[*]-(meg:Person {name:"Meg Ryan"})
)
RETURN p
```

### **Recommend** : pour recommander
Recommander de nouveaux co-acteurs potentiels à Tom Hanks avec qui il n'a pas encore joué :
```
MATCH (tom:Person {name:"Tom Hanks"})-[:ACTED_IN]->(m)<-[:ACTED_IN]-(coActors),
  (coActors)-[:ACTED_IN]->(m2)<-[:ACTED_IN]-(cocoActors)
WHERE NOT (tom)-[:ACTED_IN]->()<-[:ACTED_IN]-(cocoActors) AND tom <> cocoActors
RETURN cocoActors.name AS Recommended, count(*) AS Strength ORDER BY Strength DESC
```

Trouver quelqu'un pour présenter Tom Hanks à Tom Cruise :
```
MATCH (tom:Person {name:"Tom Hanks"})-[:ACTED_IN]->(m)<-[:ACTED_IN]-(coActors),
  (coActors)-[:ACTED_IN]->(m2)<-[:ACTED_IN]-(cruise:Person {name:"Tom Cruise"})
RETURN tom, m, coActors, m2, cruise
```