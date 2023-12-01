# Test d'utilisation d'une base de données NOSQL de type Colonne
Pour cet exercice, utilisation de l'offre gratuite de Datastax : [cliquer ici](https://www.datastax.com/fr/pricing/astra-db)

Utilisation de la version gratuite de Datastax, après inscription (besoin d'une adresse mail)

## Pré requis
Créer une base de données :

![](https://raw.githubusercontent.com/vincent2mots/bga/main/NOSQL/images/cassandra.PNG)

Télécharger également [le jeu de données suivant](http://b3d.bdpedia.fr/files/restaurants.zip), au format zip. Une fois récupéré en local, vous pouvez le dézipper.

## Exercice 1 : Créer les tables

Créer les tables suivantes : 

```
USE tpcassandra
```
```
CREATE TABLE Restaurant (
   id INT, Name VARCHAR, borough VARCHAR, BuildingNum VARCHAR, Street VARCHAR,
   ZipCode INT, Phone text, CuisineType VARCHAR,
   PRIMARY KEY ( id )
 ) ;
```
```
 CREATE INDEX fk_Restaurant_cuisine ON Restaurant ( CuisineType ) ;
```
```
 CREATE TABLE Inspection (
   idRestaurant INT, InspectionDate date, ViolationCode VARCHAR,
   ViolationDescription VARCHAR, CriticalFlag VARCHAR, Score INT, GRADE VARCHAR,
   PRIMARY KEY ( idRestaurant, InspectionDate )
 ) ;
```
```
CREATE INDEX fk_Inspection_Restaurant ON Inspection ( Grade ) ;
```

Remarquez qu'ici, on utilise le CQL (Cassandra Query Language) qui est très proche du SQL.

Vérifier le schéma des tables précédemment créées :
```
DESC Restaurant;
```
```
DESC Inspection;
```

## Exercice 2 : Import de données

