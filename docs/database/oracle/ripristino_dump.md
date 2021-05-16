
====== Ripristino del database a partire da un file di dump ======


===== Creazione tablespace =====

Se vogliamo che le tabelle del dump che stiamo per ripristinare abbiano il loro tablespace dedicato, sarà per prima cosa necessario crearlo:

<code>CREATE TABLESPACE Napoli DATAFILE '/mnt/data1/Oracle_12c/Napoli.dbf' 
SIZE 4G AUTOEXTEND ON NEXT 1G;</code>

Una volta creato, potremo indicare quel tablespace come tablespace di default per l'utente che andremo a creare, invece di utilizzare il tablespace di sistema.


===== Creazione utente =====

Per creare un utente //locale//:

<code>
CREATE USER ciro
    IDENTIFIED BY ciro123 -- assegno una password al nuovo utente
    DEFAULT TABLESPACE Napoli -- associo l'utente ad un tablespace specifico
    QUOTA UNLIMITED ON Napoli -- e imposto la quota di spazio riservata all'utente (illimitata)
    TEMPORARY TABLESPACE temp -- associo l'utente al tablespace temporaneo predefito
    QUOTA UNLIMITED ON system; -- e imposto una quota di spazio riservata all'utente (illimitata)
</code>

===== Assegnazione ruoli all'utente =====

<code>
grant "IMP_FULL_DATABASE" to ciro;
grant "EXP_FULL_DATABASE" to ciro;
</code>

===== Analisi dump =====

Prima di procedere al ripristino del dump è necessario capire quali schemi (SCHEMA o USER) contengono le tabella che vogliamo importare. Questo per limitarci a riversare le sole tabelle che ci servono ed evitare di importare i dati degli utenti di sistema.

L'analisi del dump deve essere fatta //a mano//, analizzando il file di log prodotto con un istruzione di questo tipo:

  imp system@globaldb file=/mnt/data1/Napoli_DATISORGENTE/napoli.dmp GRANTS=n 
    log=/mnt/data1/Napoli_DATISORGENTE/show_tables.log SHOW=TABLES FULL=yes


===== Ripristino dump =====

Una volta individuati gli utenti / schemi che contengono le tabelle che ci interessano, possiamo procedere al loro ripristino:

  imp system/OracleDb2013@globaldb file=/mnt/data1/Napoli_DATISORGENTE/napoli.dmp GRANTS=n 
    log=/mnt/data1/Napoli_DATISORGENTE/show_USER6899.log FROMUSER=USER6899 TOUSER=C##iro

Possiamo eventualmente specificare quali tabelle vogliamo che siano importate:

  imp system/OracleDb2013@globaldb file=/mnt/data1/Napoli_DATISORGENTE/napoli.dmp GRANTS=n 
    log=/mnt/data1/Napoli_DATISORGENTE/show_USER6899.log FROMUSER=USER6899 TOUSER=C##iro TABLES=ACCESSI


===== Nota =====
Utilizzando la versione 12c, è necessario che il nome utente sia preceduto dal prefisso C##.
