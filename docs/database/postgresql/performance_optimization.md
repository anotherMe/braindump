
## Performance optimization

[PostgreSQL wiki](https://wiki.postgresql.org/wiki/Performance_Optimization)


## Statement loggin

### When using Docker

You can just enable statement loggin by modifying the container *command*.

For example, when using Docker Compose:

```yaml
services:
    postgresql:
        image: postgres:10-alpine
        ...
        command: ["postgres", "-c", "log_statement=all"]
```

### On a runngin container

You *should* be able to change database settings using SQL:

```sql
ALTER SYSTEM SET log_statement = 'all';
SELECT pg_reload_conf();

ALTER SYSTEM RESET log_statement;
SELECT pg_reload_conf();
```