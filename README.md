# Compte Rendu

Commande magique

```shell
docker system prune -a --volumes
```

## Network
```shell
docker network create app-network
```

## Database

```shell
docker build -t mdeville/database ./database

docker run \
  --name database \
  --net=app-network\
  -e POSTGRES_DB=db \
  -e POSTGRES_USER=usr \
  -e POSTGRES_PASSWORD=pwd \
  -v database-data:/var/lib/postgresql/data \
  -v $(pwd)/database/sql:/docker-entrypoint-initdb.d:ro \
  -d \
  mdeville/database
```

## Adminer

```shell
docker run \
  -p "8090:8080" \
  --net=app-network \
  --name=adminer \
  -d \
  adminer
```

[click her to see your database](http://localhost:8090/?pgsql=database&username=usr&db=db&ns=public)

## Simple Api

```shell
docker build -t mdeville/simple-api ./simple-api

docker run \
  -p "8080:8080" \
  --net=app-network \
  --name=simple-api \
  -d \
  mdeville/simple-api
```

[click her to check your api](http://localhost:8080/departments/IRC/students)

## httpd

```shell
docker build -t mdeville/httpd ./httpd

docker run \
  -p "80:80" \
  --net=app-network \
  --name=httpd \
  -d \
  mdeville/httpd
```

```shell
docker exec -it my-front cat /usr/local/apache2/conf/httpd.conf > httpd.conf
```

[click her to check the reverse-proxy](http://localhost/departments/IRC/students)

## docker-compose 

```shell
docker compose up -d
```

```shell
docker compose down
```

Follow the logs of a specific service

```shell
docker compose logs --follow <service_name>
```


[click her to see your database with adminer](http://localhost:8090/?pgsql=database&username=usr&db=db&ns=public)
[click her to check the reverse-proxy](http://localhost/departments/IRC/students)
