
====== Install Oracle Database 11gR2 on Oracle Linux 6 ======
([[https://oracle-base.com/articles/11g/oracle-db-11gr2-installation-on-oracle-linux-6|reference]])

==== Turn off firewall ====

Based on the distro you're on, you may have to [[https://docs.oracle.com/cd/E20815_01/html/E20821/gisry.html|turn off firewall]]:

  service ipchains stop
  service iptables stop

  chkconfig ipchains off
  chkconfig iptables off
  
==== Disable SELinux ====

Set **SELinux** to permissive ( [[https://docs.fedoraproject.org/en-US/Fedora/11/html/Security-Enhanced_Linux/sect-Security-Enhanced_Linux-Working_with_SELinux-Enabling_and_Disabling_SELinux.html|Enabling and disabling SELinux]] )

==== Configure hosts ====

Set **hosts** file [[https://oracle-base.com/articles/11g/oracle-db-11gr2-installation-on-oracle-linux-6#HostsFile|host file]]


==== Install prerequisites ====

You have here two choices you can go through a step by step, manual installation or, if you are on Oracle Linux, you can simply issue:

  yum install oracle-rdbms-server-11gR2-preinstall

==== Perform additional setup ====

Perform [[https://oracle-base.com/articles/11g/oracle-db-11gr2-installation-on-oracle-linux-6#additional_setup|additional setup]]

  mkdir -p /u01/app/oracle/product/11.2.0/db_1  
  chown -R oracle:oinstall /u01
  chmod -R 775 /u01

then:

  xhost +<machine-name>
  
===== Notes =====

When switching user, remember to use the dash syntax, ie:

  su - oracle
  
Doing this you set the proper environment variables ( ie sourcing //.bashrc// and //.bash_profile// files ).
===== Issues =====

==== Error launching installer on X Access Control ====

Nonostante le istruzioni di installazione ( linkate a fondo pagina ) indichino specifiche configurazioni relative alle policies di controllo di accesso dell'X-Server ( comando //xhost// e variabile DISPLAY ), è comunque possibile che l'installer fallisca, segnalando un generico errore java.

**Soluzione**: Disabilita l'Access Control dell'X server:

  xhost +
  
  

==== Error connecting to em console ====

Al termine dell'installazione, provando a connettersi ad Enterprise Manager Console, il browser segnala questo errore:

Connessione sicura non riuscita

An error occurred during a connection to ol6.localdomain:1158. The server certificate included a public key that was too weak. (Error code: ssl_error_weak_server_cert_key) 

**Soluzione**:

  emctl unsecure dbconsole
  
__A questo punto sarà possibile accedere all'EM console tramite http ( e non più https ).__
  
==== Riferimenti ====
  
[[https://windows7bugs.wordpress.com/2015/10/11/oracle-database-11g-r2-issues-with-accessing-enterprise-manager-ssl_error_weak_server_cert_key/|ref]]