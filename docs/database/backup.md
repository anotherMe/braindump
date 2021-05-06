
====== Database backup ======


===== Backup =====

Esistono diversi modi per fare il backup di un database MySQL ma il più diffuso di questi è basato sul'utilizzo dell'utility mysqldump.

  mysqldump -u user -p db_da_copiare > backup.sql

Se la base dati da backuppare è molto grande può essere utile eseguire la compressione dell'output prodotto da mysqldump. Per farlo possiamo reindirizzare il risultato prodotto dal programma ad un utility di compressione come GZIP. Ad esempio:

  mysqldump -u user -p db_da_copiare | gzip -9 > backup.sql.gz

===== Restore =====

Una volta creata la copia di backup del nostro DB non ci resta che vedere come effettuare il ripristino. Se nel backup è presente la query per la ricreazione del database sarà sufficiente digitare:

  mysql -u user -p < backup.sql
  
Per ripristinare i dati di un backup compresso con GZIP, infine, utilizzeremo una sintassi del genere:

  gunzip < backup.sql.gz | mysql -u user -p