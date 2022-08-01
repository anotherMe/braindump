# Docker

**Note**: You always need to be careful when using the `$` character, for example you should avoid it inside passwords.


## MySQL

```bash
docker run --name marinestore-mysql -e MYSQL_ROOT_PASSWORD=secret3! -p 33006:3306 --restart unless-stopped -d mysql:5 
```

## Postgresql

Use *docker run* to launch a PostgreSQL 9 container:

```bash
docker run --name postgres9 -e POSTGRES_PASSWORD=s3cret -d --restart unless-stopped -p 5001:5432 postgres:9
```


## ActiveMQ

```bash
docker run -p 61616:61616 -p 8161:8161 rmohr/activemq:5.14.3
```

## Socat

### Expose JMX port

Given:

- MYCONTAINER - the container you want to connect to
- MYNETWORK - the docker network the container is running in ( you may omit the *network* parameter if the container is running on the default docker network )

you may expose port 1099 of MYCONTAINER:

```bash
docker run --publish 2099:1099 --network MYNETWORK --link MYCONTAINER:target alpine/socat tcp-listen:1099,fork,reuseaddr tcp-connect:target:1099
```

Note though that port 1099 on target container MUST be listening on the public interface for this command to work. If target container is listening on 127.0.0.1:1099, this will not work.


## Reclaim some space

Note: this two commands may seem a little bit disruptive ( we're trying to remove ALL the containers and ALL the images ), but docker will delete only containers and images that aren't currently in use.

```bash
docker rm $(docker ps -qa)
```

```bash
docker rmi $(docker images -q)
```
