===== WORK IN PROGRESS =====


Non sono ancora stato in grado di completare questa procedura. Per ora quindi, ripristina il dump usando la procedura "vecchia" ma utilizzando un utente di tipo C##.



====== Ripristino di un file di dump ======

===== Creazione PDB (Pluggable Database) =====

Data la nuova architettura multitenant utilizzata da Oracle 12c, prima di procedere alle operazioni di import dei dati, creaiamo prima un nuovo PDB.

<code>
CREATE PLUGGABLE DATABASE Napoli ADMIN USER Napoliadm IDENTIFIED BY ciro123
  ROLES=(DBA)  
  -- STORAGE (MAXSIZE 2G MAX_SHARED_TEMP_SIZE 100M)
  DEFAULT TABLESPACE napoli01 
  DATAFILE '/mnt/data1/Oracle_12c/Napoli_PDB/napoli01.dbf' SIZE 1G AUTOEXTEND ON
  PATH_PREFIX = '/mnt/data1/Oracle_12c/Napoli_PDB/' 
;
</code>

Questa istruzione si occupa, in un solo comando, di creare e configurare utente e tablespace e di associarli al PDB appena creato.

==== Apertura del PDB in read/write mode ====

Una volta creato il nuovo PDB è possibile verificare il suo stato con il comando:

    select * from V$PDBS;

Appena creato, il nuovo PDB si trova in stato //MOUNTED//, è necessario metterlo in stato //READ WRITE//.

Per modificare lo stato del PDB è prima necessario connettersi al container all'interno del quale è stato creato il PDB, utilizzando, ad esempio, una normale sessione di SqlPlus o SqlDeveloper, con il solito utente SYS AS SYSDBA.
  
Una volta connessi al container è necessario modificare la sessione per spostarsi sul PDB creato (in questo caso //Napoli//):

  alter session set container = napoli;

e quindi modificare lo stato del database:

  ALTER PLUGGABLE DATABASE OPEN READ WRITE;

===== Creazione utente =====

Per creare un utente //locale// all'interno del pluggable database, ci connettiamo al container esterno e poi ci spostiamo sul PDB:

<code>
alter session set container = napoli;
 
 CREATE USER ciro 
    IDENTIFIED BY ciro123
    QUOTA UNLIMITED ON system
    CONTAINER=CURRENT; -- questa riga specifica che si tratta di utente local e non common
</code>

===== Assegnazione ruoli all'utente =====

<code>
grant "IMP_FULL_DATABASE" to ciro;
grant "EXP_FULL_DATABASE" to ciro;
</code>