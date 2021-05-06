# Showing and changing interface address

Display IP Addresses and property information for all devices:

  # ip addr show

Display IP Addresses and property information for device em1:

  # ip addr show em1

Assign IP to interface:

  # ip addr add 192.168.50.5 dev eth1

Delete IP from interface:

  # ip addr del 192.168.50.5/24 dev eth1

Enable interface:

  # ip link set eth1 up

Disable interface:

  # ip link set eth1 down


# Showing and changing routing table

## Show routing table

  # ip route

Show the route a specific address X.X.X.X will take according to current routing table:

  # ip route get X.X.X.X

## Add / remove route

Given a multihomed host with three network interfaces:

<code>
lo: inet 127.0.0.1/8 scope host lo
ens32: inet 192.168.24.201/24 brd 192.168.24.255 scope global ens32
ens34: inet 192.168.1.201/24 brd 255.255.255.255 scope global ens34
ens35: inet 192.168.0.201/24 brd 255.255.255.255 scope global ens35
</code>

and following routing table:

<code>
default via 192.168.24.50 dev ens32 onlink
192.168.0.0/24 dev ens35  proto kernel  scope link  src 192.168.0.201
192.168.1.0/24 dev ens34  proto kernel  scope link  src 192.168.1.201
192.168.24.0/24 dev ens32  proto kernel  scope link  src 192.168.24.201
</code>

You can add a new temporary* entry to table, to route all traffic toward 212.97.32.0-255 through network interface //ens35// like this:

  # ip route add 212.97.32.0/24 via 192.168.1.1 src 192.168.1.201

The **via** parameter should point to the gateway IP ( ie: the router IP )

The **src** parameter set the //source IP address// of each packet originating from your host. It is mandatory in order to assure that returning traffic is correctly routed to originating IP address ( see [[https://serverfault.com/questions/451601/ip-route-show-src-field|here]] for further details ).

/*
 * 
 * 
 *     Facendo alcune verifiche, impostando una nuova rotta per tentare di scaricare il file http://test.kpnqwest.it/file2000.bin utilizzando un'interfaccia di rete specifica, risulta che il comando:
 *       
 *       # ip route add 212.97.32.17 dev ens34
 * 
 *     setta la rotta:
 * 
 *      212.97.32.17 dev ens34  scope link
 *      
 *     ma che questa rotta non consente di effettuare un traceroute ( verso test.kpnqwest.it ) e tantomeno un download.
 * 
 *     Il comando:
 * 
 *       # ip route add 212.97.32.17 dev ens34 src 192.168.1.201 
 * 
 *    nuovamente setta una rotta che non consente il download del file.
 * 
 *     Invece, il comando:
 * 
 *       # ip route add 212.97.32.17 via 192.168.1.1 src 192.168.1.201 dev ens34
 * 
 *     che setta anche il parametro **src** e che risulta nella rotta seguente:
 * 
 *       212.97.32.17 via 192.168.1.1 dev ens34  src 192.168.1.201
 * 
 *     permette di effettuare il traceroute ed il download.
 * 
 * 
*/

To delete the above route:

  # ip route del 212.97.32.0/24

Replace, or add if not defined, a given route:

  # ip route replace 192.168.1.0/24 via 192.168.1.1


#### Footnotes

<nowiki>*</nowiki> To make routing table changes permanent, you have to edit the appropriate files ( eg: /etc/sysconfig/network/routes or /etc/network/interfaces )