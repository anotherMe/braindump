# UFW - Uncomplicated FireWall

## Examples

Allow SNMP traffic:

  # ufw allow snmp

Deny SNMP traffic:

  # ufw deny snmp

Rules are removed by prepending //remove// key word to rule:

  # ufw remove deny snmp

Allow SNMP traffic from given host, given proto and comment :

<code>
# ufw allow from 192.168.10.0/24 to any proto udp port 161 \
comment "Allow SNMP checks from FOOHOST"
</code>


By default, ufw will apply rules to all available interfaces. To
limit  this,  specify DIRECTION on INTERFACE, where DIRECTION is
one of **in** or **out** (interface aliases  are  not  supported).   For
example,  to  allow  all  new incoming http connections on eth0,
use:

  ufw allow in on eth0 to any port 80 proto tcp
