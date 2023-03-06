# Informations importantes

**Ce projet est utilisé à des fins éducatives. NE PAS utiliser en production !**


# Configuration :

## Environnement

Dans le fichier [.env](.env), mettre à jour la valeur **APP_ECV_DIR** pour correspondre à la racine du projet en valeur relative.
Modifier les valeurs du fichier **db.ecv.env** et/ou **postgres_ecv.env** si besoin.

Beaucoup de variables d'environnement liées aux ports, nom de domaine et versions sont également modifiables.

# Lancement

```
docker compose -f docker-compose.yaml up --build
```

# Accéder aux containers

## Via le navigateur

- Nginx : http://localhost ou http://localhost:8081
- Caddy : https://localhost
- Symfony Serveur http://localhost:8000
- Mailcatcher : http://localhost:1080
- PhpMyAdmin : http://localhost:8036
- Adminer : http://localhost:8037
- pgAdmin : http://localhost:8038

## Via un terminal (comme une connexion ssh)

Container PHP qui servira à lancer les lignes de commandes Symfony, Composer ... :
 ```shell script
docker exec -it ecv_php /bin/bash
 ```

Container Node pour la partie CSS, JS :
 ```shell script
docker exec -it ecv_node /bin/ash
 ```

# Commandes diverses :

**Depuis ce dossier :**
 - Reconstruire le container PHP :
Commenter *image:* , décommenter *build:* puis lancer le build
 ```
 docker compose -f docker-compose.yaml build
 ```
 - Lancer les containers du projet :
 ```
 docker compose -f docker-compose.yaml up
 ```

**Depuis n'importe où :**
 - Arrêter tous les containers :
 ```
 docker stop $(docker ps -q)
 ``` 
 - Supprimer tous les containers :
 ```
 docker rm $(docker ps -a -q)
 ``` 
 - Supprimer toutes les images
 ```
 docker rmi $(docker images -q)
 ```
