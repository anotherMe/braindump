# SNMP - Simple Network Management Protocol

SNMP is an Internet-standard __protocol__ for collecting and organizing information about managed devices on IP networks and for modifying that information to change device behavior.

SNMP exposes management data in the form of variables on the managed systems, organized in a [[https://it.wikipedia.org/wiki/Management_Information_Base|management information base]] (**MIB**) which describe the system status and configuration.

Three significant versions of SNMP have been developed and deployed. SNMPv1 is the original version of the protocol. More recent versions, SNMPv2c and SNMPv3, feature improvements in performance, flexibility and security.


## Testing functionality with snmpwalk

You can check if SNMP agent is reachable and is working using **snmpwalk**. 

In the following example, we test SNMP service on host //foohost// using protocol version //2c// and //public// community:

  snmpwalk -v 2c -c public foohost

We haven't passed an **OID**, so we are querying the whole tree. Alternatively you can start walking down the tree starting from given node:

  snmpwalk -v 2c -c public foohost system

or:

  snmpwalk -v 2c -c public foohost .1.3.6.1.4.1


## An example: monitor disk space

Standard installations of the SNMP agent, as per //snmpd.conf// defaults, usually expose the system portion of the tree ( OID value = 1.3.6.1.2.1.1 ).

To add disk monitoring functionality we should refere to the [[http://oid-info.com/get/1.3.6.1.4.1.2021.9|1.3.6.1.4.1.2021.9.1]] portion of the tree.

So, on the host where the SNMPd agent runs, we add the following lines to ///etc/snmp/snmpd.conf// file:

<code>
view    systemview    included   .1.3.6.1.4.1.2021.9.1
# Check the / partition and make sure it contains at least 5 Gigabytes
disk /data 5000000
</code>

Now you should be able to query the snmp server from a remote host with 
something like this:

  snmpwalk -c public -v 2c MYHOSTNAMEORIP .1.3.6.1.4.1.2021.9.1


### References

* [[http://net-snmp.sourceforge.net|Net-SNMP Sourceforge project page]]
* [[http://oid-info.com/|Object Identifier (OID) Repository]]
* [[http://www.mibdepot.com/index.shtml|MIB Depot]]
* [[http://www.oidview.com/mibs|OID View]]

