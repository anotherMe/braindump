
Following commands must be issued from *psql* console:

```bash
$ sudo su - postgres
$ psql
```


## Create a new user

```sql
CREATE ROLE myuser LOGIN ;
-- or
CREATE USER myuser;
```

Set a password :

```sql
alter role myuser password 'password!';
```
  


## Create database

```sql
create database MYDATABASE;
```
