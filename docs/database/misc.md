
# Count all tables

```sql
select concat('select ''', TABLE_NAME, ''' as table_name, count(*) from ', TABLE_NAME, ' union all') from information_schema.TABLES t where TABLE_SCHEMA = 'getrin';
```

