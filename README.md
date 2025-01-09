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