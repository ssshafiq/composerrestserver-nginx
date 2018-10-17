
## MTBC HYPERLEDGER REST SERVER NGINX
=======



###  ENVIRONMENT VARIABLES

Create and edit envvars.txt FILE 

```
COMPOSER_CARD=alice@med-net
COMPOSER_NAMESPACES=never
COMPOSER_AUTHENTICATION=true
COMPOSER_MULTIUSER=true
COMPOSER_PROVIDERS='{
  "github": {
    "provider": "github",
    "module": "passport-github",
    "clientID": "653ec5dcb75aa9bebddc",
    "clientSecret": "e10b713553ec423bc327978c755abc912268492c",
    "authPath": "/auth/github",
    "callbackURL": "/auth/github/callback",
    "successRedirect": "http://10.10.30.188:4200?loggedIn=true",
    "failureRedirect": "/"
  }
}'


COMPOSER_DATASOURCES='{
    "db": {
        "name": "db",
        "connector": "mongodb",
        "host": "mongo"
    }
}'



```


run following command

```
source envvars.txt
```


###  DOCKER BUILD COMMANDS

Go inside dockertemp directory and run following command

```
docker build -t myorg/composer-rest-server .
```

run this commnad to docker run

```
docker run \
    -d \
    -e COMPOSER_CARD=${COMPOSER_CARD} \
    -e COMPOSER_NAMESPACES=${COMPOSER_NAMESPACES} \
    -e COMPOSER_PROVIDERS="${COMPOSER_PROVIDERS}" \
    -e COMPOSER_DATASOURCES="${COMPOSER_DATASOURCES}" \
    -v ~/.composer:/home/composer/.composer \
    --name rest1 \
    --network composer_default \
    -p 3001:3000 \
    myorg/my-composer-rest-server
```

change port and name to run multiple containers

### BUILD NGIXN IMAGE

go inside ngixnAuth and run following command

```
docker build -r nginxauth .
```
run following commnad to run nginx

```
docker run -d -p 5001:5001 nginxauth
```