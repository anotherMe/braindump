
====== Importazione dati da file di dump ======

L'importazione dati da un file di dump ( effettuato tramite //exp// o //expdp// ) si esegue utilizzando lo strumento **impdp** ( o il suo predecessore, ora deprecato, **imp** ). 

Un file di dump prodotto con **expdp** può essere ripristinato solo con **impdp** mentre un dump prodotto con **exp** può essere ripristinato solo con **imp**.

===== Analisi =====

Il primo passo da compiere prima di procedere con il ripristino vero e proprio è quello di raccogliere informazioni sul contenuto del dump ovvero sugli schemi e sulle tabelle in esso contenuti, nonché su eventuali riferimenti a specifici tablespace.

Tipicamente un file di dump creato tramite **expdp** ( o **exp** ) si accompagna ad un file di log, in cui sono presenti le informazioni che cerchiamo.

In mancanza di questo file, è necessario recuperarle dal dump stesso. Per le relative istruzioni, fai riferimento a [[recupero_informazioni|questa pagina]].

===== Ripristino =====

Una volta completata la ricognizione, è possibile procedere al [[ripristino|ripristino vero e proprio]]. 

[[ripristino_dump|Qui]] trovi invece istruzioni per effettuare il ripristino tramite il deprecato //imp//.

**Nota**: per i più temerari, avevo iniziato ad abbozzare istruzioni per il [[ripristino_dump_12c|ripristino su di un'istanza Oracle 12c]].

