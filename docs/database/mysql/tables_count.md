

```sql

-- OKKIO al limite delle 200 righe !

drop table if exists tables_count;
create table tables_count ( id int auto_increment, table_name varchar(64), conteggio int, PRIMARY KEY (id) );

select concat('insert into tables_count (table_name, conteggio) select ''', TABLE_NAME,''', count(*) from ', table_name  ,';') 
from information_schema.TABLES t where TABLE_SCHEMA = schema() and TABLE_TYPE = 'BASE TABLE';

select * from tables_count order by conteggio desc;

select * from tables_count_20221025 t1
left join tables_count_20221026 t2 on t1.table_name = t2.table_name
where t1.conteggio != t2.conteggio;

```



