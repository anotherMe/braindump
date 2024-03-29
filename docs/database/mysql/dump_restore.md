
# Dump


Esistono diversi modi per fare il backup di un database MySQL ma il più diffuso di questi è basato sul'utilizzo dell'utility mysqldump.

```bash
mysqldump -u <USER> -p <SCHEMA> > backup.sql
```
  

Se la base dati da backuppare è molto grande può essere utile eseguire la compressione dell'output prodotto da mysqldump. Per farlo possiamo reindirizzare il risultato prodotto dal programma ad un utility di compressione come GZIP. Ad esempio:
  
```bash
mysqldump -u user -p db_da_copiare | gzip -9 > backup.sql.gz
```

## Dump structure only of given table

```bash
mysqldump -u <USER> -p <SCHEMA> --no-data --skip-add-drop-table <TABLE_ONE> <TABLE_TWO> ... > dump.sql
```


# Restore

Una volta creata la copia di backup del nostro DB non ci resta che vedere come effettuare il ripristino. Se nel backup è presente la query per la ricreazione del database sarà sufficiente digitare:

  
```bash
mysql -u user -p < backup.sql
```
  
Per ripristinare i dati di un backup compresso con GZIP, infine, utilizzeremo una sintassi del genere:

```bash
gunzip < backup.sql.gz | mysql -u user -p
```
  

## Restoring dump with blobs

Trying to restore of a dump containing long lines and/or blobs, got error `MySQL Error 1153 - Got a packet bigger than 'max_allowed_packet' bytes`.

As per [this Stackoverflow post](https://stackoverflow.com/questions/93128/mysql-error-1153-got-a-packet-bigger-than-max-allowed-packet-bytes), I had to change some system variables on the database:

```sql
set global net_buffer_length=1000000; 
set global max_allowed_packet=1000000000;
```

