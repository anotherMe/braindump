
# SSH tunneling

( [reference](https:chamibuddhika.wordpress.com/2012/03/21/ssh-tunnelling-explained) )

## Local port forwarding

We have three machines:

- **work** ( your workstation at office )
- **bridge** ( reachable; outside firewall, eg: your home computer )
- **remotehost** ( not reachable from office because of proxy / firewall )

With SSH, we can reach for **remotehost** tunneling traffic through bridge host:

To tunnel HTTP traffic between work and remotehost, we just need to run this command ( __on work host__ ):

```bash
# ssh myuser@bridge -L 0.0.0.0:9001:remotehost:80
```

In the above command, we start a new SSH instance on the work host, listening on port 9001. When connecting to that port ( ie: pointing work web browser to address http:127.0.0.1:9001 ), we are tunneling our HTTP traffic through bridge host and, eventually, to port 80 of remotehost.


## Reverse tunnelling with remote port forwarding

Now, the other way around: from outside your corporate firewall, eg: from your home computer, you can't reach your office workstation.

* **intranet** ( host not reachable from outside because of corporate proxy / firewall )
* **bridge** ( reachable on the internet with public address; you have root access to this machine )
* **homepc**

Execute this command from **intranet** host:

```bash
# ssh -R 0.0.0.0:8080:localhost:80 root@example.bridge.org
```

when you're back home, pointing your browser to http://example.bridge.or:8080, will give access to port 80 of your office machine

Note that to have SSH listening on 0.0.0.0, you need to run the command as *root* and maybe set some other options in your SSH daemon configuration ( eg: /etc/ssh/sshd_config ):

```
    PermitRootLogin yes
    GatewayPorts yes
```


## Dynamic port forwarding

Suppose the same scenario imagined in the first example:

* **work** ( your workstation at office )
* **bridge** ( reachable; outside firewall, eg: your home computer )
* **remotehost** ( not reachable because of proxy / firewall )

What if, instead of a single protocol, we would like to tunnel __all__ type of traffic ? We could do that by creating a SOCKS proxy.


Here SSH will create a SOCKS proxy listening in for connections at local port 9001:

  $ ssh -D 9001 home (__ executed from work )



### Useful flags

**-N** - Do not execute a remote command.  This is useful for just forwarding ports.
