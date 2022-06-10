

```sql
select * from information_schema.PROCESSLIST p
order by db, time;

select * from information_schema.PROCESSLIST p 
where db = 'costa_certificazione' order by time;
```

