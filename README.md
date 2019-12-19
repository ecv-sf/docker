# Configuration :

## Nginx

Changer la valeur du server_name à la ligne 3 du fichier [container/nginx/ecv.conf](./container/nginx/ecv.conf)

## Environnement

Dans le fichier [.env](.env), mettre à jour la valeur **APP_ECV_DIR** pour correspondre à la racine du projet en valeur relative.
Modifier les valeurs du fichier **db.ecv.env** si besoin

# Lancement

```
docker-compose -f docker-compose.yaml up
```

# Container

- Mailcatcher : http://localhost:1080
- PhpMyAdmin : http://localhost:8036
- Adminer : http://localhost:8037
- Nginx : http://*server_name* ou http://localhost:8081