
===== Enable remote access (step 1) =====

Make daemon listen on external IP addresses, editing the //**listen_addresses**// parameter on //**postgresql.conf**// file.

On a debian machine, edit the file:

  # vi /etc/postgresql/9.4/main/postgresql.conf

Modifying the parameter //**listen_addresses**// to something like this, based on your network architecture:

> listen_addresses = '192.168.10.77' # listen to the interface with IP 192.168.10.77

**NOTE**: The above address is the IP of the Postgres database server, the address __to listen on__.

===== Enable remote access (step 2) =====

Client authentication is controlled by a configuration file, which traditionally is named **pg_hba.conf** which is usually stored in the database cluster's data directory.

<code># vi /etc/postgresql/9.4/main/pg_hba.conf # Debian default location</code>
<code># vi /var/lib/pgsql/data/pg_hba.conf # Red Hat default location</code>

For detailed instruction about how to edit this file, refer to the comments inside the file itself. 

Add / edit an //host// line, like one of the following:

<code>
#	host	DATABASE	USER	ADDRESS
	host	all  		all	192.168.10.1/24  trust
</code>

Trust all connections (no password) on the given IP range.


After changing //pg%%_%%hba.conf//, you need to trigger a server configuration reload using **pg_ctl** or by stopping and restarting the server process:

<code>pg_ctl reload [-D datadir]</code>
