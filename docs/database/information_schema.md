
# Count all tables

```sql
select concat('select ''', TABLE_NAME, ''' as table_name, count(*) from ', TABLE_NAME, ' union all') from information_schema.TABLES t where TABLE_SCHEMA = 'XXX';
```


# Check / optimize / analyze tables


```sql
select concat('check table ', TABLE_NAME, ';') from information_schema.TABLES t where TABLE_SCHEMA = 'XXX';
select concat('optimize table ', TABLE_NAME, ';') from information_schema.TABLES t where TABLE_SCHEMA = 'XXX';
select concat('analyze table ', TABLE_NAME, ';') from information_schema.TABLES t where TABLE_SCHEMA = 'XXX';
```

