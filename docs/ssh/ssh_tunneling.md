
# SSH tunneling
( [[https://chamibuddhika.wordpress.com/2012/03/21/ssh-tunnelling-explained/|reference]] )

## Local port forwarding

We have three machines:

* **work** ( your workstation at office )
* **bridge** ( reachable; outside firewall, eg: your home computer )
* **remotehost** ( not reachable because of proxy / firewall )

Suppose that //**work**// can't reach //**remotehost**// ( eg: because //work// is a workstation behind a corporate proxy/firewall that blocks traffic to //remotehost// ). With SSH, we can reach for //remotehost// tunneling traffic through //bridge// host:

To tunnel HTTP traffic between //work// and //remotehost//, we just need to run this command ( __on //work// host__ ):

  # ssh myuser@bridge -L 0.0.0.0:9001:remotehost:80

In the above command, we start a new SSH instance on the //work// host, listening on port 9001. When connecting to that port ( ie: pointing //work// web browser to address http://127.0.0.1:9001 ), we are tunneling our HTTP traffic through //bridge// host and, eventually, to port 80 of //remotehost//.

## Reverse tunnelling with remote port forwarding

Now, the other way around: from outside your corporate firewall, eg: from your home computer, you can't reach one of your company servers.

* **work**
* **bridge** ( behind firewall, eg: your office workstation )
* **intranethost**

Execute this command ( __ from //work// host__ ):

  # ssh -R 9001:intranethost:80 home

when you're back home, pointing your browser to http://127.0.0.1:9001, will give access to port 80 of //intranethost//.


## Dynamic port forwarding

Suppose the same scenario imagined in the first example:

* **work** ( your workstation at office )
* **bridge** ( reachable; outside firewall, eg: your home computer )
* **remotehost** ( not reachable because of proxy / firewall )

What if, instead of a single protocol, we would like to tunnel __all__ type of traffic ? We could do that by creating a SOCKS proxy.


Here SSH will create a SOCKS proxy listening in for connections at local port 9001:

  $ ssh -D 9001 home (__ executed from //work// )



### Useful flags

**-N** - Do not execute a remote command.  This is useful for just forwarding ports.
