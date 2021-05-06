
====== Avvio e arresto manuale ======

=== Nota preliminare ===

Tutte le procedure seguenti vanno eseguite come utente **oracle**:

  su - oracle
  
Aprendo una sessione come utente //oracle// ( __non dimenticarti il segno meno nel comando sopra !__ ), si avranno infatti configurate correttamente tutte le variabili d'ambiente.

---

===== Avvio =====

==== Enterprise Manager Console ====

Avvio di Enterprise Manager Console:

  emctl start dbconsole

==== Listener ====

Avvio del listener:

  lsnrctl start
  
==== Istanza ====

Per avviare l'istanza Oracle è possibile utilizzare l'interfaccia web ( Enterprise Manager Console ) o, in alternativa **SQLPlus**:

  sqlplus /nolog

  SQL> connect / as sysdba
  SQL> startup

===== Arresto =====

==== Enterprise Manager Console ====

==== Istanza ====

Per arrestare l'istanza Oracle è possibile utilizzare l'interfaccia web ( Enterprise Manager Console ) o, in alternativa **SQLPlus**:

  sqlplus /nolog

  SQL> connect / as sysdba
  SQL> shutdown immediate
  
Arresto di Enterprise Manager Console:

  emctl stop dbconsole

==== Listener ====

Arresto del listener:

  lsnrctl stop
  
