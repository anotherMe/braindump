

====== Esportazione dati su file di dump ======

La migrazione dei dati da un istanza Oracle ad un altra viene abitualmente effettuata tramite strumento **expdp** ( o tramite il suo predecessore, ora obsoleto, **exp** ).

**NOTA**: Ricordo che anche il consulente Mario D'Afiero, durante l'esportazione dati effettuati presso la provincia di Salerno, nonostante le precedenti ipotesi di utilizzo di backup **RMAN** e relativo spostamento dei file di configurazione ( es: init.ora ), aveva valutato come più efficace, semplice e solido l'utilizzo di exp.


===== Lo strumento expdp =====

---

==== esempio 1 ====

Ci connettiamo come utente system per esportare i dati dello schema //IPA_ADRIATICO//:

<code bash>expdp system/singularity15 DUMPFILE=test.dmp SCHEMAS=IPA_ADRIATICO</code>

=== DATA_PUMP_DIR ===

Il parametro DUMPFILE non permette di specificare un path, ma solo un nome di file. Nell'istruzione riportata sopra, il file di dump verrà quindi nella directory utilizzata di default di datapump:

<code sql>select * from all_directories where directory_name = 'DATA_PUMP_DIR';</code>

Nel nostro caso, la directory si trovava sul percorso:

  /u01/app/oracle/admin/orcl/dpdump


Eventualmente è possibile passare il parametro \\DIRECTORY\\ per specificare un percorso diverso da quello di default:

<code bash>expdp system/singularity15 DUMPFILE=test.dmp SCHEMAS=IPA_ADRIATICO DIRECTORY=MyDirectory</code>

dove //MyDirectory// non rappresenta un percorso fisico ma un //oggetto directory//, che come tale va prima creato ( [[http://www.orafaq.com/wiki/Datapump#Create_database_directories|vedi qui]] ).

---
==== esempio 2 ====

Nell'istruzione seguente, ci connettiamo utilizzando l'utente //system//, e procediamo all'esportazione dello schema //IPA_ADRIATICO//:

<code bash>expdp system/oicsRAC2010  SCHEMAS=ipa_adriatico DUMPFILE=ipa_adriatico-$(date +%Y%m%d%H).dmp LOGFILE=ipa_adriaticoLOG-$(date +%Y%m%d%H).log</code>

---
===== Lo strumento exp (deprecato) =====

Mi connetto come utente system per effettuare un dump completo ( tutti gli schemi ):

  exp system/singularity15 FILE=/home/oracle/test.dmp FULL=y


Mi connetto come utente system per effettuare un dump del solo schema //IPA_ADRIATICO//:

  exp system/singularity15 FILE=/home/oracle/test.dmp OWNER=IPA_ADRIATICO
