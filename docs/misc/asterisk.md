
# Asterisk

## Accessing the console

With the command

  asterisk -r

you can connect to a running Asterisk process and get a console interface to it.

# Asterisk CLI commands for troubleshooting

## Getting started

To view current settings:

  core show settings
  
To change verbosity level:

  core set verbose X

where X is an integer between 0 and 10 ( or even more ).


## Show queue subscriptions

Show status and subscriptions of a specified queue:

  queue show XXX

where XXX is the queue number; omit to show informations for all queues.

## Show active calls

  core show channels

## Show IAX2 peers

  iax2 show peers

## Show SIP peers

  sip show peers

## Show DAHDI informations

  dahdi show status
  dahdi show channels


## Log file

  cat /var/log/asterisk/messages
  cat /var/log/asterisk/full
  

### Reference

* [[http://www.asteriskdocs.org/en/2nd_Edition/asterisk-book-html-chunk/index.html|Asterisk™: The Future of Telephony 2nd ed.]]
* [[http://www.asteriskdocs.org/en/3rd_Edition/asterisk-book-html-chunk|Asterisk™: The Definitive Guide 3rd ed.]]
* [[http://wiki.freepbx.org/display/FOP/Hangup+Cause+Codes|Hangup Cause Codes]]

### Glossary

* **Asterisk** is a software implementation of a telephone private branch exchange (**//PBX//**); it allows attached telephones to make calls to one another, and to connect to other telephone services, such as the public switched telephone network (PSTN) and Voice over Internet Protocol (VoIP) services.

* **FreePBX** is a web-based open source graphical user interface (GUI) that manages Asterisk, a voice over IP and telephony server.

* **DHADI** Digium Asterisk Hardware Device Interface is a collection of open source drivers, for linux, that are used to interface with a variety of telephony related hardware

* **Inter-Asterisk eXchange (IAX)** is a communications protocol native to the Asterisk private branch exchange (PBX) software, and is supported by a few other softswitches, PBX systems, and softphones. It is used for transporting VoIP telephony sessions between servers and to terminal devices. The original IAX protocol is deprecated and has been superseded by a second version, commonly called IAX2.

