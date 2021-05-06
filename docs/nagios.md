# Nagios

Install & config instructions for a fresh, text only, Ubuntu 16 Server installation. Refer to  [[https://help.ubuntu.com/lts/serverguide/nagios.html|Ubuntu wiki - Nagios]]) for details.


## Installation

### Main host

  # apt install nagios3 nagios-nrpe-plugin

During installation you'll be asked for //nagiosadmin// password. 

Subsequently, you can change that password by issuing:

  # htpasswd /etc/nagios3/htpasswd.users nagiosadmin
  
To add another user:

  # htpasswd /etc/nagios3/htpasswd.users steve


### Remote host

  # apt install nagios-nrpe-server nagios-plugins


## Add a new host with simple DNS monitoring

On the Nagios server, create a configuration file for the new host:

  # vi /etc/nagios3/conf.d/mytarget.cfg

The file should look something like this:

<file>
define host{
	use generic-host ; Name of host template to use
	host_name mytarget ; target host name
	alias Server 02
	address 172.18.100.101 ; IP of target host
}

# check DNS service.
define service {
	use generic-service
	host_name mytarget
	service_description DNS
	check_command check_dns!172.18.100.101
}
</file>

  # systemctl restart nagios3.service


## Configure NRPE to check disk space on target host

On the **Nagios server**, add a new service to the file ///etc/nagios3/conf.d/mytarget.cfg//:

<file>
# NRPE disk check.
define service {
        use generic-service
        host_name mytarget
        service_description nrpe-disk
        check_command check_nrpe_1arg!check_all_disks!172.18.100.101
}
</file>

On the **target host**, edit file **/etc/nagios/nrpe.cfg** to allow remote connection from Nagios server:

<file>allowed_hosts=172.18.100.100</file>

and to add a new command:

<file>command[check_all_disks]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -e</file>

And restart NRPE service:

  # /etc/init.d/nagios-nrpe-server restart


## How to install new plugins

First make sure you cannot find wanted plugin in the [[http://packages.ubuntu.com|repository]]. If not available, manually download the script to folder **/usr/lib/nagios/plugins**.

Change permission:

  sudo chown root:root /usr/lib/nagios/plugins/my_plugin.sh
  sudo chmod a+x /usr/lib/nagios/plugins/my_plugin.sh

Then edit **/etc/nagios-plugins/config/snap.cfg** to  assign each command_line a correspondent command_name:

<code>
define command{
    command_name    snmp_load
    command_line    /usr/lib/nagios/plugins/check_snmp -H '$HOSTADDRESS$' -C '$ARG1$' -o .$
    }
</code>

## Set hostgroup image 
##### ( Ubuntu 16.04 )

By defining an **hostexinfo**, you can assign nice images to every hosts. Path of images is relative to the logos folder of the web site; in Ubuntu it's:

  /usr/share/nagios3/htdocs/images/logos/

NOTE: You can put your own images in that folder, just remember that, for best result, the right size is 40x40 pixels. To convert png images to gd2 format, you'll have to use **pngtogd2** (in Ubuntu shipped inside package //libgd-tools// ).

## Email notifications
##### ( Ubuntu 16.04 )

First step is adding a new contact and, possibly, add the contact to a contact group. Contacts and contact groups are defined by default in **/etc/nagios3/conf.d/contacts_nagios2.cfg** file.

On Debian based distro we can do that by editing:

  # vi /etc/nagios3/conf.d/contacts_nagios2.cfg
  
Now we can link our contacts / contact groups to our hosts or services. In the example below, we are going to notify all the contacts in the //admins// group when something happens to one of our hosts. Let's modify the file **/etc/nagios3/conf.d/myhost_nagios2.cfg**:


<code>
define host{
        use                     generic-host
        host_name               myhost
        alias                   myhostalias
        address                 192.168.666.666
        contact_groups          admins
        }
</code>

The relevant configuration parameter here is **contact_groups**.


### References

[[http://www.thegeekstuff.com/2009/06/4-steps-to-define-nagios-contacts-with-email-and-pager-notification/|The geek stuff]]

[[https://www.ftmon.org/blog/nagios-notification-setup-testing|Nagios Notification Setup And Testing]]

[[https://assets.nagios.com/downloads/nagioscore/docs/nagioscore/3/en/notifications.html|Nagios documentation - notifications]]
