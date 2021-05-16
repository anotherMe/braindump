# Docker

**Note**: You always need to be careful when using the `$` character, for example you should avoid it inside passwords.

## Postgresql

Use *docker run* to launch a PostgreSQL 9 container:

```bash
docker run --name postgres9 -e POSTGRES_PASSWORD=s3cret -d --restart unless-stopped -p 5001:5432 postgres:9
```



