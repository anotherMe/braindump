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

