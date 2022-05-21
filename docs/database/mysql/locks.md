
# Locks

If a query hangs, and it's showing in **Waiting for table metadata lock** state in the *Sessions*:

```sql
SHOW processlist;
```

you can try to check DB engine status:

```sql
show engine innodb status;
```

or maybe reach for some more details from these tables:

```sql
SELECT * from information_schema.INNODB_LOCK_WAITS;

SELECT * from information_schema.INNODB_LOCKS il;

SELECT * FROM information_schema.INNODB_TRX;
```

