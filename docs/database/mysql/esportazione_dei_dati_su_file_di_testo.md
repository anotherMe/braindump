
# Esportazione dei dati su file di testo

Di seguito uno script per riversare i dati della tabella TABELLA_SORGENTE nel file CSV chiamato FILE_DESTINAZIONE.csv:

```sql
select *
INTO OUTFILE '/mnt/data1/dump/FILE_DESTINAZIONE.csv'
FIELDS TERMINATED BY '\t' escaped by ' '
-- OPTIONALLY ENCLOSED BY '"' -- ESCAPED BY 'X'
LINES TERMINATED BY '\n' 
from TABELLA_SORGENTE;
```


Nota le istruzioni //**escaped by**//, che servono a specificare un carattere sostitutivo se per caso nei campi di testo della tabella dovesse essere presente lo stesso carattere che vogliamo utilizzare come terminatore di riga o di campo o altro.


Ref: [](https://dev.mysql.com/doc/refman/5.7/en/select-into.html)