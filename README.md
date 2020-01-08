# Configuration :

## Nginx

Changer la valeur du server_name à la ligne 3 du fichier [container/nginx/ecv.conf](./container/nginx/ecv.conf)

Si vous utilisez un server_name différent de localhost, pensez à l'ajouter dans le fichier /etc/hosts (ou C:\windows\system32\drivers\etc\hosts)

```
127.0.0.1    mon-site.local
```

## Environnement

Dans le fichier [.env](.env), mettre à jour la valeur **APP_ECV_DIR** pour correspondre à la racine du projet en valeur relative.
Modifier les valeurs du fichier **db.ecv.env** si besoin

# Lancement

```
docker-compose -f docker-compose.yaml up
```



# Accéder aux containers

## Via le navigateur

- Mailcatcher : http://localhost:1080
- PhpMyAdmin : http://localhost:8036
- Adminer : http://localhost:8037
- Nginx : http://*server_name* ou http://localhost:8081

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
 - Reconstruire les containers : 
 ```
 docker-compose -f docker-compose.yaml build
 ```
 - Lancer les containers du projet :
 ```
 docker-compose -f docker-compose.yaml up
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
