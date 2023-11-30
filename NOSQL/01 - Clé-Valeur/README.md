# Test d'utilisation d'une base de données NOSQL de type Clé-Valeur
Pour cet exercice, utilisation de la sandbox Redis (Bac à sable), disponible ici gratuitement : [cliquer ici](https://try.redis.io/){:target="_blank"}
 
## Exercice 1

1. Créer la clé **User** avec comme valeur **Dario**
<details>
  <summary>Solution</summary>

```
set User Dario
```

</details>





## Exercice 1 : Ecriture / Lecture simple dans Redis
Insertion d'une clef avec sa valeur associée dans la base de données Redis :
```
set clef "valeur"
```

Récupération de la valeur : 
```
get clef
```

## Exercice 2 : Ecriture d'une valeur avec une date d'expiration
La commande SET nous propose des options sur le comportement de la clé et sur le comportement de l'insertion :
- On peut définir une expiration en secondes avec EX ou en millisecondes avec PX. Ex : SET clef valeur EX 5.
- On peut définir une condition d'insertion NX (définie la clé-valeur seulement si elle n'existe pas) ou XX (définie la clé-valeur seulement si elle existe déjà).


```
set clef "valeur" EX 10
```

Récupération de la valeur 10 secondes plus tard : 
```
get clef
```

Au bout des 10 secondes, la commande *get clef* devrait retourner (nil). Cela indique que la donnée n'est plus disponible car expirée