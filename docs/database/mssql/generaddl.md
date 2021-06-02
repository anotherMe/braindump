====== Migrazione degli schemi ======

Il primo passo per riversare i dati da un database Oracle ad un database MSSQL è quello di ricreare la stessa struttura dati, ovvero gli stessi schemi e le stesse tabelle, sul database di destinazione.

===== Procedura automatica =====

Sono disponibili strumenti automatizzati per effettuare la migrazione degli schemi da Oracle a MSSQL, come il 
[SQL Server Migration Assistant for Oracle](https://msdn.microsoft.com/en-us/library/hh313159.aspx) .

Lo strumento in passato mi ha dato problemi ( di installazione ) e quindi non sono ancora riuscito a sfruttarlo come si dovrebbe. Vale la pena fare un tentativo prima di passare alla più laboriosa ed artigianale procedura *manuale*.



===== Procedura manuale =====

La generazione delle istruzioni DDL, può essere effettuata utilizzando lo strumento **Oracle SQL Developer**.

Per farlo è possibile selezionare le tabelle desiderate e poi, tramite il menù contestuale, selezionare il comando **DDL rapido** oppure **Esporta ...** .

Utilizzando il comando **Esporta ...**, avendo cura di deselezionare, per il momento, l'opzione di esportazione dei dati, avremo la possibilità di selezionare alcune opzioni che ci consentiranno di generare codice SQL più pulito e quindi più semplice da trasformare in codice MSSQL.

Ecco di seguito un esempio di configurazione:

{{:oracle:crea_ddl.png?200|}}

===== Modifica DDL =====

Lo script DDL creato utilizza chiaramente la sintassi Oracle. Per convertirlo in formato MSSQL, è quindi necessario effettuare un po' di trova&sostituisci per adeguare la sintassi e, soprattutto, per adeguare i tipi delle colonne.


