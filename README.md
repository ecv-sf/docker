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

# Container

- Mailcatcher : http://localhost:1080
- PhpMyAdmin : http://localhost:8036
- Adminer : http://localhost:8037
- Nginx : http://*server_name* ou http://localhost:8081
