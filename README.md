# devops_trainning_devb
<i> Fait par Léo Brevière </i>

## Question 1

installer docker

## Question 2

créer repository

## Question 3
### .A
cmd : 
```bash
docker pull httpd
```

rsp :
```
Using default tag: latest
latest: Pulling from library/httpd
fd674058ff8f: Already exists
8c3081b233c7: Pull complete
4f4fb700ef54: Pull complete
172b239db5c2: Pull complete
bbff13f6be42: Pull complete
d7382fd3e491: Pull complete
Digest: sha256:72f6e24600718dddef131de7cb5b31496b05c5af41e9db8707df371859a350bb
Status: Downloaded newer image for httpd:latest
docker.io/library/httpd:latest
```

### .B
cmd :
```bash
docker images
```

rsp :
```
REPOSITORY        TAG       IMAGE ID       CREATED         SIZE
httpd             latest    4ce47c750a58   5 months ago    147MB
postgis/postgis   14-3.3    80f3732b16e2   17 months ago   586MB
```

### .C
cmd : 
```bash
mkdir html 
cd html
touch index.html
cd ..
```

ctn de index.html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
hello world
</body>
</html>
```

### .D

cmd :
```bash
docker run -d -p 80:80 -v  ${PWD}/html:/usr/local/apache2/htdocs/ --name httpd httpd
```

rsp : 
```
eca35fd740e318a20ef03fcee635f657b50292ec56ea6aa481b70c4d55c93a2b
```
### .E

 - Stop : 


cmd : 
```bash
 docker stop eca35fd740e318a20ef03fcee635f657b50292ec56ea6aa481b70c4d55c93a2b
```

rsp : 
```
eca35fd740e318a20ef03fcee635f657b50292ec56ea6aa481b70c4d55c93a2b
```

- Suprimer

cmd :
```bash
  docker rmeca35fd740e318a20ef03fcee635f657b50292ec56ea6aa481b70c4d55c93a2b
```

rsp :
```
eca35fd740e318a20ef03fcee635f657b50292ec56ea6aa481b70c4d55c93a2b
```

### .F

- Lancer :


cmd :
```bash
docker run -d -p 80:80 httpd
```

rsp :
```
c368d3f4f84d5e0e7101309e806161b77c838fb4de157f2e2c0130757f306659
```

- Copier les fichiers

cmd :
```bash
docker cp ${PWD}/html/index.html c368d3f4f84d5e0e7101309e806161b77c838fb4de157f2e2c0130757f306659:/usr/local/apache2/htdocs/

```

rsp :
```
Successfully copied 2.05kB to c368d3f4f84d5e0e7101309e806161b77c838fb4de157f2e2c0130757f306659:/usr/local/apache2/htdocs/
```

## Question 4
### .A

- create Dockerfile

### .B

- construction image

cmd :
```bash
 docker build -t my-img .
```

rsp :
```
[+] Building 1.9s (7/7) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                                                                           0.0s
 => => transferring dockerfile: 118B                                                                                                                                                                                           0.0s 
 => [internal] load .dockerignore                                                                                                                                                                                              0.0s 
 => => transferring context: 2B                                                                                                                                                                                                0.0s 
 => [internal] load metadata for docker.io/library/httpd:latest                                                                                                                                                                1.9s 
 => [1/2] FROM docker.io/library/httpd:latest@sha256:72f6e24600718dddef131de7cb5b31496b05c5af41e9db8707df371859a350bb                                                                                                          0.0s
 => => resolve docker.io/library/httpd:latest@sha256:72f6e24600718dddef131de7cb5b31496b05c5af41e9db8707df371859a350bb                                                                                                          0.0s 
 => [internal] load build context                                                                                                                                                                                              0.0s 
 => => transferring context: 61B                                                                                                                                                                                               0.0s 
 => CACHED [2/2] COPY ./html/ /usr/local/apache2/htdocs/                                                                                                                                                                       0.0s 
 => exporting to image                                                                                                                                                                                                         0.0s 
 => => exporting layers                                                                                                                                                                                                        0.0s 
 => => writing image sha256:c5719fc6a66d59f373acd4faf5c25b9d10cea03f8be1f2417d2384248b2fbc86                                                                                                                                   0.0s 
 => => naming to docker.io/library/my-img
 ```

- construction image

cmd :
```bash
docker run -d -p 80:80 my-img
```

rsp :
```
dbb11a91fd3cc5176ca856b3037fc93de94636d94d908801e52fb52a9b2ba28c
 ```

### .C

| **Critère**                  | **Montage de Volume (`-v`)**                     | **`COPY` dans le Dockerfile**                      |
|------------------------------|-------------------------------------------------|--------------------------------------------------|
| **Développement local**      | 👍 Idéal : Dynamique et rapide à modifier.        | 👎 Moins pratique : Nécessite de reconstruire.   |
| **Déploiement en production**| 👎 Pas recommandé : Dépend du système hôte.       | 👍 Idéal : Reproductible et indépendant.         |
| **Reproductibilité**         | 👎 Dépend des fichiers locaux et du chemin.      | 👍 Garantit des images reproductibles.           |
| **Performance**              | 👎 Peut être plus lent (surtout sur Windows).    | 👍 Performant : Pas de dépendance au système.    |
| **Taille de l'image**        | 👍 Pas d'impact sur la taille de l'image.        | 👎 Augmente si de gros fichiers sont copiés.     |


## Question 4
### .A

- Pour MySQL :

```
docker pull mysql
```


- Pour phpMyAdmin :

```
docker pull phpmyadmin/phpmyadmin
```

### B.

1. Créer un réseau Docker :
   ```
   docker network create my-net
   ```

2. Lancer un container MySQL :
   ```
   docker run -d --name <msqyl-container-name> --network <network-name> -e MYSQL_ROOT_PASSWORD=root mysql
   ```
3. Lancer un container phpMyAdmin :
   ```
   docker run -d --name <phpmyadmin-container> --network <network-name> -p 8080:80 -e PMA_HOST=mysql-container phpmyadmin/phpmyadmin
   ```
4. Accéder à phpMyAdmin via le navigateur à l'adresse : `http://localhost:8080`

## Question 6
### .A

- **Commandes Docker classiques** :

    - Nécessitent de lancer chaque container individuellement.
    - La gestion des réseaux et des variables d'environnement peut être fastidieuse.

- **Fichier docker-compose.yml** :

    - Permet de définir les services (containers), réseaux, et volumes dans un seul fichier.
    - Simplifie le déploiement grâce à une seule commande pour démarrer ou arrêter tous les services.

### .B

- **Lancer les containers** :
  ```
  docker-compose up -d
  ```
- **Arrêter les containers** :
  ```
  docker-compose down
  ```

### .C

```yaml
version: '3.8'
services:
  mysql:
    image: mysql
    container_name: mysql-container
    environment:
      MYSQL_ROOT_PASSWORD: root
    networks:
      - db-network

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: phpmyadmin-container
    ports:
      - "8080:80"
    environment:
      PMA_HOST: mysql-container
    networks:
      - db-network

networks:
  db-network:
    driver: bridge
```