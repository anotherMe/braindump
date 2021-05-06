====== Active directory ======


===== How to test active directory credentials =====

==== Problem ====

On a Windows platform, is there any command line utility that I can pass a username, password domain name to in order to verify the credentials (or possibly give an error that the account is disabled, doesn't exist or expired)?

==== Solution ====

You could use the net use command, specifying the username and password on the command-line.

Try to mount net share:

<code>net use X: \\192.168.23.151\dati\GEOGAS\SCANSIONI /user:GASIT\scannermi23 Password$1</code>

Unmount:

<code>net use X: /d</code>

([[http://serverfault.com/questions/410240/is-there-a-windows-command-line-utility-to-verify-user-credentials|source]])

