# Influxdb

## Start

```sh
cd fluxdb
docker-compose up -d
```

## Stop

```sh
docker-compose down
```

## Enter influxdb running in Docker

`local_influxdb` is your container name.

```sh
docker exec -it local_influxdb bin/bash
```

## Start InfluxDB

Access InfluxDB using [welcome](localhost:8086/onboarding/0) and go through the initial setup.

You have to create a user, password, and organization, which can be anything to your liking.

You will also need to create a bucket (database) to store your data. This can also be anything (you can delete, create other buckets, etc. later).

After completing the above step, you will be shown an API password with superuser privileges. Save it in a safe location. You may not need it often, but when needed, you will have it.

API token: `JrvNNdsDhkemhSlfsrniq3ibKY1y6C7ylRwgEPCIg84vnqmwQlnxUw0kd4z3lgbR-QrgajP20pKbiIas1X9Y4Q==`
