
Create user/schema:

```sql
CREATE USER my_user IDENTIFIED BY my_password
DEFAULT TABLESPACE users
QUOTA 100M ON users;
```

Grant privileges:

```sql
GRANT CREATE SESSION, CREATE TABLE, CREATE VIEW, CREATE SEQUENCE TO my_user;
```

Grant additional permission (if needed):

```sql
ALTER USER my_user QUOTA UNLIMITED ON users;
```