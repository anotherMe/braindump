# Samba 

## Installazione e configurazione

**Nota**: La maggior parte delle operazioni seguenti possono essere
eseguite tramite Webmin se disponibile.

Installare Samba Server e sue dipendenze.

Creare un nuovo gruppo utente sul sitema operativo denominato, ad 
esempio, //foogroup// .

Creare un nuovo gruppo utente Samba, utilizzando lo stesso nome 
( quindi //foogroup// ) e mapparlo su quello di sistema.

Creare un utente di sistema, chiamarlo ad esempio //foouser//, impostare 
"No Login Allowed".

Non impostare una password, non "creare" nulla (home page, ecc ecc)
Metterlo nel gruppo //foogroup// invece che //users// .

Tramite l'apposita funzionalità di Webmin / Samba, migrare gli utenti dal
sistema operativo a Samba e infine impostare loro una password.


## Gestione e manutenzione

Report on current Samba connections:

  smbstatus


Check //smb.conf// configuration file for internal correctness:

  testparm

Test connection:

  smbclient //mysambaserver/mysharedfolder -U mysambauser



