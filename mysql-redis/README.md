# Mysql and Redis

## Start

```sh
cd mysql-redis
docker-compose up -d
```

## Stop

```sh
docker-compose down
```

## 通过容器名进入（适用于 docker run 启动的容器）

```sh
docker exec -it mysql8 mysql -u root -p
```

## 通过 docker-compose 进入（推荐）

```sh
docker-compose exec mysql8 mysql -u root -p
```
