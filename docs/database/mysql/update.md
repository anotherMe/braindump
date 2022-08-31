
## MySQL update join syntax:

```sql
UPDATE tableA a
INNER JOIN tableB b ON a.name_a = b.name_b
SET validation_check = if(start_dts > end_dts, 'VALID', '')
-- where clause can go here
```



## ANSI SQL syntax:

```sql
UPDATE tableA SET validation_check = 
    (SELECT if(start_DTS > end_DTS, 'VALID', '') AS validation_check
        FROM tableA
        INNER JOIN tableB ON name_A = name_B
        WHERE id_A = tableA.id_A)
```

