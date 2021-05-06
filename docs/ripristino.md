
=====Ripristino del file di dump=====

Dopo aver effettuato l'[[recupero_informazioni|analisi del dump]], avendo individuato i vari **schemi** presenti nel dump ed i relativi **tablespaces**, possiamo procedere al recupero dei dati.

---

=== Nota preliminare ===

Tutti i files, di input e di output, cui si fa riferimento nelle varie istruzioni elencate di seguito, a partire dal file di dump, devono trovarsi nella cartella di datapump di default ( ad esempio, /opt/oracle/admin/oradb/dpdump ); diversamente è necessario indicare ad impdp un **[[oggetto directory|oggetto_directory]]** alternativo.

---

In uno scenario tipico il ripristino, anche di un dump che contiene al suo interno più schemi, viene effettuato uno schema alla volta. Qui sotto, ad esempio, utilizziamo il parametro SCHEMAS per specificare che il ripristino verrà limitato al solo schema //ART16//:

  impdp SYSTEM/password@oradb DUMPFILE=SIL.dmp \
  SCHEMAS=ART16 REMAP_SCHEMA=ART16:Sicilia_ART16 \
  REMAP_TABLESPACE=TS_ART16_DATA:SICILIA \
  LOGFILE=Import_ART16.log


==== Remapping degli schemi ====

Se lo schema che stiamo importando non esiste nel database di destinazione, dovremo procedere a **rimappare lo schema**:

  REMAP_SCHEMA=schema_sorgente:schema_destinazione

==== Remapping dei tablespaces ====

Potrebbe inoltre essere necessario **rimappare il tablespace** ( o i tablespaces ):

  REMAP_TABLESPACE=tablespace_sorgente:tablespace_destinazione


==== Sovrascrittura delle tabelle ====

Durante le operazioni di ripristino può capitare di dover lanciare più volte lo script di import. Per evitare di dover svuotare gli schemi ogni volta è possibile specificare il parametro **TABLE_EXISTS_ACTION**:

  TABLE_EXISTS_ACTION={SKIP | APPEND | TRUNCATE | REPLACE}

===== Issues =====

La procedura di importazione dei dati a partire da file di dump, può richiedere talvolta interventi di tipo "manuale". Di seguito, elenco alcuni di questi casi.

==== tablespace ====

Una prima, tipica problematica in cui si può incorrere è quella in cui, nel dump da ripristinare, si faccia riferimento ai //tablespace// ( un //tablespace// è un'entità astratta, che fa riferimento ad uno o più file di dati fisici ) su cui dovranno essere allocati tabelle e indici. 

In un caso del genere sarà necessario ricreare gli stessi tablespace ( leggi: con lo stesso nome ) sull'istanza di destinazione o, in alternativa, tramite la relativa opzione di imp, rimappare il tablespace:

<code>REMAP_TABLESPACE=src1:dst1 REMAP_TABLESPACE=src2:dst2</code>

==== riferimenti incrociati ====

Un'altra problematica tipica della procedura di ripristino tramite imp è causata dalla presenza di più schemi con riferimenti incrociati ( ad esempio, una foreign key sullo schema X che punta ad una tabella sullo schema Y ). In un caso del genere, l'ordine con cui si effettua il ripristino non può essere casuale: sarà necessario importare prima lo schema Y e, successivamente, lo schema X.

===== References =====

[[https://docs.oracle.com/cd/E11882_01/server.112/e22490/dp_import.htm#SUTIL300|Oracle 11gR2 (11.2) - Data Pump Import]]

[[https://docs.oracle.com/cd/E11882_01/server.112/e25494/toc.htm|Oracle 11gR2 (11.2) - Database Administrator's Guide]]