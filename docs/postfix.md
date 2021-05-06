# Postfix #


## Install ##

For detailed installation instructions, refer to following links:

[[https://www.digitalocean.com/community/tutorials/how-to-install-and-setup-postfix-on-ubuntu-14-04|This]] article explains how to install and configure Postfix on Ubuntu.

[[https://www.digitalocean.com/community/tutorials/why-you-may-not-want-to-run-your-own-mail-server|This]] article explains //Why You May Not Want To Run Your Own Mail Server//, but provides a nice overview of all the components of a mail server.

## Disable local delivery

You should remove $mydomain from your mydestination in **main.cf**. That way postfix will just relay it on using MX lookups.


## How to enable port 587 (submission) in postfix

To enable port 587, edit the file /etc/postfix/master.cf

  vi /etc/postfix/master.cf

and uncomment the line ( you may actually have to modify it ): 

  submission inet n - y - - smtpd

and restart postfix:

  /etc/init.d/postfix restart


## The main.cf file ##

Some notes on the //main.cf// configuration file.

### mydestination ###

The **mydestination** parameter specifies what domains this machine will deliver locally, instead of forwarding to another machine.

Example:

  myhostname = vrtmail03.gas.it
  mydestination = $myhostname, mail03.gas.it, vrtmail03.gas.it, localhost.gas.it, localhost


### mynetworks ###

By default, Postfix will forward mail from clients in authorized network blocks to any destination. Authorized networks are defined with the **mynetworks** configuration parameter.


## Testing 1 ##

With telnet and XCLIENT:

see [[http://www.postfix.org/XCLIENT_README.html|Postfix XCLIENT Howto]]

## Testing 2 ##

On my local machine, which resides on the same network of the Postfix server, I created a new outgoing server (SMTP) in Thunderbird ( Options / Account settings ):

{{:server_smtp.png?400|}}

Now I create a new identity, linking it to the newly created SMTP server. 

{{postfix:new_identity.png?400|}}

Even using a pre-exisistent account, if I can now try to send mail. Just rememeber to use to correct identity:

{{:composizione.png?400|}}

If mynetworks parameter has been setup right:

  mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128 192.168.2.0/24
  
we could even send mail to external recipients ( ex: mytestaccount@gmail.com ).


## SASL Authentication ##

We are going to configure our server to use //**Cyrus SASL**// ( with the //**sasldb backend plugin**// ) on our //Ubuntu Server// box ( see [[sasl|here]] for info about managing users database ).

Install needed pacakges:

  $ apt install libsasl2-2 sasl2-bin libsasl2-modules

Edit SASL daemon configuration file **/etc/default/saslauthd**:

  START=yes
  DESC="SASL Authentication Daemon"
  NAME="saslauthd"
  MECHANISMS="sasldb"
  MECH_OPTIONS=""
  THREADS=5
  OPTIONS="-c -m /var/spool/postfix/var/run/saslauthd" # we are running a chrooted Postfix

Note the **START**, **MECHANISMS** and **OPTIONS** parameters.

Edit Postfix configuration file **/etc/postfix/main.cf** adding / modfying the lines:

  # Cyrus SASL configuration
  smtpd_sasl_auth_enable = yes
  smtpd_sasl_path = cyrus # Cyrus SASL configuration file name ( actual file is cyrus.conf )
  smtpd_sasl_local_domain = 
  smtpd_sasl_security_options = noanonymous
  broken_sasl_auth_clients = yes
  smtpd_recipient_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination


Note the **smtpd_sasl_path** parameter. This one set the name of the configuration file we are going to create:

  # vi /etc/postfix/sasl/cyrus.conf
  
and edit like this:

  pwcheck_method: auxprop
  auxprop_plugin: sasldb
  mech_list: PLAIN LOGIN CRAM-MD5 DIGEST-MD5 NTLM


Because Postfix needs **/etc/sasldb2** in his chroot environment, we may change the init script to copy sasldb2 at startup.

We do that by editing **/etc/init.d/postfix**, and adding //etc/sasldb2// in the variable FILES :
	
  FILES="etc/localtime etc/services etc/resolv.conf etc/hosts \
    etc/host.conf etc/nsswitch.conf etc/nss_mdns.config etc/sasldb2"



### References

[[http://www.postfix.org/SASL_README.html|Postfix documentation - SASL]]

[[https://help.ubuntu.com/community/Postfix#Authentication|Ubuntu help - Postfix]]

[[https://wiki.debian.org/PostfixAndSASL|Debian wiki - Postfix and SASL]]


## Monitoring

###  Dump all messages in queue ( deferred and pending )

  mailq

or

  postqueue -p

### qshape

Print Postfix queue distribution.

To see distribution for //deferred// queue:

  # qshape deferred


## Maintenance

### Delete queued mail (!)

Delete all queued mail

  # postsuper -d ALL

Delete only the deferred mail queue messages (i.e. only the ones the system intends to retry later)

  # postsuper -d ALL deferred

