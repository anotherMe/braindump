
=====L'oggetto directory=====

Se non diversamento specificato, tutti file cui fanno riferimento i parametri di impdp sono relativi alla cartella di datapump di default ( di solito, /opt/oracle/admin/oradb/dpdump/ ).

Per utilizzare percorsi alternativi è necessario indicare ad impdp un **oggetto directory** ( e non un percorso fisico ) da utilizzare.

Ciò può essere fatto globalmente:

    impdp DIRECTORY=\mia\data\dir DUMPFILE=SIL.dmp LOGFILE=SIL.log

e, in tal caso tutti i file faranno riferimento alla directory di base specificata; oppure, di volta in volta, anteponendo l'oggetto directory ai vari parametri:

    impdp DUMPFILE=miadatadir:SIL.dmp