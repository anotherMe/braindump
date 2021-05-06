# Esportare i dati su file CSV

Per esportare il contenuto delle tabelle, la strada più semplice è quella di utilizzare la procedura guidata messa a disposizione dallo strumento Oracle SQL Developer ( Strumenti \ Esportazione database ... ) .

Prima di procedere, è opportuno **modificare le impostazioni di localizzazione** ( lingua, formato date, valuta, etc ... ) per semplificare al massimo il successivo riversamento da CSV a MSSQL.

## Formattazione date

La più importante delle impostazioni di localizzazione da verificare ed eventualmente modificare è quella relativa al **formato delle date**.

Per modificarlo, richiamare la funzionalità dal menu Strumenti \ Preferenze e poi Database \ NLS:

{{:wiki:sqldeveloper_nls_options.png?auto|}}

Nota che il **Formato data** è stato modificato per includere anche minuti, secondi, etc.

## Dump

Una volta verificate le impostazioni di base è possibile procedere con il dump dei files. Di seguito un esempio di configurazione da utilizzare:

{{:wiki:sqldeveloper_databaseexport.png?auto|}}