### Test de recherche de données dans Elasticsearch

Ici, la solution présenter est Opensearch : il s'agit d'un fork réalisé par Amazon (AWS) basé sur Elasticsearch (avec, donc, le même langage d'interrogation de données)

Procédure à suivre : 
- URL à laquelle se connecter **depuis le VPN Next Decision** : http://192.168.2.150:5601/ avec le compte **admin** / **admin**
- Se rendre dans le Dev Tools : http://192.168.2.150:5601/app/dev_tools#/console

Exécuter les recherches suivantes dans Elasticsearch : 

```
# Chercher tous les documents qui contiennent le mot "fox"
# SQL : select * from library where title like '%fox%'
GET /library/_search
{
  "query": {
    "match": {
      "title": "fox"
    }
  }
}

 # Essayons en cherchant "quick" et "dog" (Type match) : https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-match-query.html 
 GET /library/_search
 {
  "query": {
    "match": {
      "title": "quick dog"
    }
  }
 }
 
 # Utilisation de match_phrase : on cherche exactement "quick dog"
 GET /library/_search
 {
  "query": {
    "match_phrase": {
      "title": "quick dog"
    }
  }
 }
 
 # Les résultats sont retournés triés par pertinence
 GET /library/_search
 {
  "query": {
    "match": {
      "title": "quick"
    }
  }
 }
 
 # Recherche avec des caractères spéciaux 
GET /library/_search
 {
  "query": {
    "wildcard": {
      "title": {
        "value": "*ump*"
      }
    }
  }
 }
 
 # Recherche floue "fuzzy"
 # max_expansions à 50 par défaut : le nombre de permutations maximal
 GET /library/_search
 {
   "query": {
     "fuzzy": {
       "title": {
         "value": "box" 
       }
     }
   }
 } 

  # Les combinatoires peuvent être boostées :
 # Ici, on accorde 3 fois plus d'importance à "lazy dog" qu'à "quick dog"
 GET /library/_search
 {
  "query": {
    "bool": {
      "should": [
        {
          "match_phrase": {
            "title": {
              "query": "quick dog"
            }
          }
        },
        {
          "match_phrase": {
            "title": {
              "query": "lazy dog" ,
              "boost": 3
            }
          }
        }
      ]
    }
  }
 }  
 ```