# redis-sentinel

[![dockeri.co](http://dockeri.co/image/lgatica/redis-sentinel)](https://hub.docker.com/r/lgatica/redis-sentinel/)

[![Build Status](https://travis-ci.org/lgaticaq/redis-sentinel.svg?branch=master)](https://travis-ci.org/lgaticaq/redis-sentinel)

> Docker image of redis sentinel from official redis alpine image

Supported tags and respective Dockerfile links

- 4.0.2, 4.0, 4, latest ([4.0/Dockerfile](https://github.com/lgaticaq/redis-sentinel/blob/master/4.0.2/Dockerfile))
- 3.2.11, 3.2, 3 ([3.2/Dockerfile](https://github.com/lgaticaq/redis-sentinel/blob/master/3.2.11/Dockerfile))

## Usage with docker run
```shell
docker run -d --name redis-sentinel-01 --link some-redis:master -p 32801:26379 lgatica/redis-sentinel
docker run -d --name redis-sentinel-02 --link some-redis:master -p 32802:26379 lgatica/redis-sentinel
docker run -d --name redis-sentinel-03 --link some-redis:master -p 32803:26379 lgatica/redis-sentinel
# Or with AUTH
docker run -d --name redis-sentinel-01 --link some-redis:master -p 32801:26379 -e REDIS_PASSWORD=redis1234 lgatica/redis-sentinel
```

## Usage with docker-compose
```yaml
version: '2'

services:
  master:
    image: redis:4.0.2-alpine
    command: redis-server --appendonly yes --masterauth $REDIS_PASSWORD --requirepass $REDIS_PASSWORD
    volumes:
      - $PWD/data/master:/data
  slave:
    image: redis:4.0.2-alpine
    command: redis-server --appendonly yes --slaveof master 6379 --masterauth $REDIS_PASSWORD --requirepass $REDIS_PASSWORD
    volumes:
      - $PWD/data/slave:/data
    depends_on:
      - master
    links:
      - master
  sentinel:
    image: lgatica/redis-sentinel
    environment:
      REDIS_PASSWORD: $REDIS_PASSWORD
    depends_on:
      - master
    links:
      - master
    ports:
      - "26379"
```
