====== Bulk insert ======

La procedura di import dati da file CSV potrebbe essere effettuata utilizzando gli strumenti GUI integrati di SQL Management Studio. Tuttavia è una procedura che sconsiglio in quanto non sufficientemente solida nè configurabile e, soprattutto, perché lenta. Di solito è infatti necessario lanciare la procedura più e più volte, attraverso una serie di approssimazioni successive. Ultimo, ma non meno importante, i veri uomini non usano strumenti GUI.

Quindi in presenza di file CSV esportati come da procedura descritta negli step precedenti, potrebbe essere sufficiente utilizzare un'istruzione del tipo:

<code>bulk insert CAMP_CLASSIFICAZIONE.TAB_ATECOLIV2
from '\\vettgeswsfs01\Bak.Sql\Bak.Sql_vETTGESWSSQL07-SQL2012DEV\Salerno - import Link\CAMP_CLASSIFICAZIONE\TAB_ATECOLIV2_DATA_TABLE.dsv'
with ( fieldterminator = '§§' )
go</code>

dove, l'unico parametro passato è quello del delimitatore di campo ("§§").


Nel caso l'esportazione sia stata effettuata diversamente, ad esempio utilizzando un codepage differente, o un terminatore di riga differente, o altro, sarà necessario specificare più parametri. Riporto di seguito un'istruzione di esempio:

<code>
bulk insert [FigureProfessionali].[RepertorioCalabria]
from '\\vettgeswsfs01\Bak.Sql\Bak.Sql_vETTGESWSSQL04-SQL2008R2DEV\Repertorio_Calabria_proposte_revisioneETT.csv'
with ( 
	 FIELDTERMINATOR = '§'
	,firstrow = 2
	,rowterminator = '\r'
	,codepage = 'ACP'
	--,DATAFILETYPE = 'widechar' -- { 'char' | 'native' | 'widechar' | 'widenative' }
)
go
</code>


