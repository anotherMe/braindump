

```sql

select count(*) from information_schema.PROCESSLIST;

select * from information_schema.PROCESSLIST p order by db, time;

select db, left(p.host, position(':' in host) - 1) as host, count(*)
from information_schema.PROCESSLIST p  
group by db, left(p.host, position(':' in host) - 1);

select left(p.host, position(':' in host) - 1) as host, count(*)
from information_schema.PROCESSLIST p  where db = 'psl'
group by left(p.host, position(':' in host) - 1);

select db, count(*) from information_schema.PROCESSLIST p  
group by db order by count(*) desc;

select count(*) from information_schema.PROCESSLIST p ;

select * from information_schema.PROCESSLIST p where DB = 'priano';

show open tables in priano;
```

