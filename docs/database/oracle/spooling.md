====== Spooling ======

Lo spooling permette di redirezionare l'output di uno script su di un dato file. E' possibile utilizzare questa funzione per effettuare il dump dei dati di un database oracle su files CSV.

  set heading off
  set echo off
  set feedback off
  set linesize 32767
  set pagesize 0
  set trimspool on
  set term off
  SET VERIFY off
  SET SPACE 0
  
  spool ' /home/oracle/ETT/spool/APPOLAVSICILIA.ext'
  
  select * from SICILIA_SILL.APPOLAVSICILIA;
  
  spool off

==== Caratteri inusuali ====

In base al set di caratteri utilizzato dal programma client, come ad esempio potrebbe essere **sqlplus**, il database Oracle può non essere in grado di produrre certi caratteri ( es: chr(167) ovvero § ).

Se, ad esempio, tentando di produrre un dump di dati in formato CSV, utilizzando come separatore il carattere **chr(167)** ( ovvero **§** ), il file di testo risultante mostrasse solo dei punti di domanda, è possibile che sia necessario modificare la variabile di ambiente NLS_LANG.

Per far ciò:

  export NLS_LANG=Italian.UTF8
  sqlplus sys/password@oradb as sysdba


==== SQLPlus e spooling ====

Solitamente, dopo aver creato lo script di spooling ( utilizzando l'apposita procedura ), lo lanciamo direttamente dalla macchina host.

Ovvero copiamo lo script SQL sulla macchina ( es: mySpool.sql ) e poi lo lanciamo con l'istruzione:

  sqlplus system/OracleDb2013@oradb @mySpool.sql


=== CLOB data type ===

CLOB data type cannot bo spooled, so it has to converted:

<code>dbms_lob.substr( MY_CLOB_COLUMN, 4000, 1 )</code>

or

<code>dbms_lob.substr( MY_CLOB_COLUMN, 32000, 1 )</code>

----


Very long CLOB data ( ie: an XML ) could require to be exported (one by one) like this:

<code>DBMS_XSLPROCESSOR.clob2file(data, 'XMLFILES_DIR', 'FILENAME.xml');</code>

where:

  * **data** is the CLOB data to be exported
  * **XMLFILES_DIR** is the name of a directory object that must have been created (NOTE: the name is case-sensitive and must be put between single quotes )
  * **FILENAME.xml** is the name of the output file

