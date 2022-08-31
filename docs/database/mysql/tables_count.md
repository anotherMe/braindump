

```sql

-- OKKIO al limite delle 200 righe !

create table tables_count ( id int auto_increment, table_name varchar(64), conteggio int, PRIMARY KEY (id) );

select concat('insert into tables_count (table_name, conteggio) select ''', TABLE_NAME,''', count(*) from ', table_name  ,';') 
from information_schema.TABLES t where TABLE_SCHEMA = :my_table_schema and TABLE_TYPE = 'BASE TABLE';

```



