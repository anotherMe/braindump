
====== Analisi del dump tramite impdp ======

ref: [[http://docs.oracle.com/cd/B28359_01/server.111/b28319/dp_import.htm|Documentazione ufficiale Oracle]]


=== Nota preliminare ===

Tutti i files, di input e di output, cui si fa riferimento nelle varie istruzioni elencate di seguito, a partire dal file di dump, devono trovarsi nella cartella di datapump di default ( ad esempio, /opt/oracle/admin/oradb/dpdump ); diversamente è necessario indicare ad impdp un **[[oggetto directory|oggetto_directory]]** alternativo.

---

La soluzione più semplice per ottenere informazioni sul contenuto del dump ( utenti, tabelle, etc ... ) è quella di generare un file DDL e poi analizzarlo:

<code bash>impdp system/mysecurepassword DUMPFILE=SIL.dmp SQLFILE=ddl.sql</code>

Il parametro //SQLFILE// indica che non dovrà essere eseguito il ripristino dei dati, ma dovranno solamente essere generate le istruzioni Data Definition Language (DDL).


===INCLUDE=== 

Volendo, per comodità, è poi possibile limitare lo script di generazione ai soli oggetti di interesse. Qui di seguito, utilizzando il parametro //INCLUDE//, recuperiamo le sole istruzioni per la creazione degli utenti:

<code bash>impdp DUMPFILE=SIL.dmp SQLFILE=ddl.sql INCLUDE=user</code>

Qui invece generiamo lo script DDL per le sole tabelle:

<code bash>impdp DUMPFILE=SIL.dmp INCLUDE="DATABASE_EXPORT/SCHEMA/TABLE/TABLE" SQLFILE=ddl.sql</code> 

Reference: [[http://docs.oracle.com/cd/B28359_01/server.111/b28319/dp_import.htm#i1007761|Documentazione ufficiale Oracle]]

===SCHEMAS===

Volendo poi rifinire ulteriormente l'informazione, possiamo limitare la generazione del DDL ad uno o più utenti/schemi di interesse.

Qui, ad esempio, generiamo lo script DDL come visto sopra, ma limitandoci, in questo caso, ad uno specifico utente ( come specificato dal parametro //SCHEMA// ):

<code bash>impdp DUMPFILE=SIL.dmp SQLFILE=ddl.sql SCHEMAS=SILL INCLUDE=tablespace</code>

==== LOGFILE ====

Per redirezionare l'output del comando su di un file in modo da salvare le informazioni ottenute, usiamo il parametro //LOGFILE//:

    impdp DUMPFILE=SIL.dmp SQLFILE=ddl.sql SCHEMAS=SILL INCLUDE=tablespace 
    LOGFILE=SILL.tablespaces.log
