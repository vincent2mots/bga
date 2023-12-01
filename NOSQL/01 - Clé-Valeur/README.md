# Test d'utilisation d'une base de données NOSQL de type Clé-Valeur
Pour cet exercice, utilisation de la sandbox Redis (Bac à sable), disponible ici gratuitement : [cliquer ici](https://try.redis.io/)

## Exercice 1

1. Créer la clé **User** avec comme valeur **Dario**
> <details>
>   <summary>Solution</summary>
> 
> ```
> set User Dario
> ```
> 
> </details>
> 
> Pour voir le contenu de la clef User : 
> ```
> get User
> ```

2. Tester la commande suivante pour renommer la clé :
> ```
> RENAME User User:1
> ```
> 
> Chercher la valeur de la nouvelle clef

3. Tester les commandes suivantes pour renommer la clé et analyser leur résultat :
> ```
> SET User:2 Toto
> ```
> ```
> RENAME User:1 User:2
> ```
> ```
> GET User:1
> ```
> ```
> EXISTS User:1
> ```
> ```
> GET User:2
> ```
> ```
> SET User:3 Toto
> ```
> ```
> RENAMENX User:3 User:2
> ```
> ```
> GET User:3
> ```
> ```
> GET User:2
> ```
> ```
> RENAMENX User:3 User:1
> ```
> ```
> GET User:1
> ```
> ```
> EXISTS User:3
> ```

4. Créer, **avec une seule commande**, les 2 clés suivantes (cf. commande **MSET**)
  * User:3 avec comme valeur Maud
  * User:4 avec comme valeur Xavier
> <details>
>   <summary>Solution</summary>
> 
> ```
> mset User:3 Maud User:4 Xavier
> ```
> 
> </details>

5. Lister toutes les clés définies dans la base (cf. commande **KEYS**)
> <details>
>   <summary>Solution</summary>
> 
> ```
> keys *
> ```
> 
> </details>

6. Lister toutes les clés commençant par User User:3
> <details>
>   <summary>Solution</summary>
> 
> ```
> keys User:3*
> ```
> 
> </details>

7. Lister les valeurs des différentes clés (cf. command **MGET**)
> <details>
>   <summary>Solution</summary>
> 
> ```
> mget User:1 User:2 User:3
> ```
> 
> </details>

8. Ajouter un 'e' à la fin de valeur de la clé User:1 (cf. command **SETRANGE**)
> <details>
>   <summary>Solution</summary>
> 
> ```
> setrange User:1 4 "e"
> ```
> 
> </details>

> Vérifier le résultat avec la commande :
> ```
> get User:1
> ```

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