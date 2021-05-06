====== CentOS 7 ======

===== Install ifconfig =====

Linux has pretty much deprecated the ifconfig command, which may have been what you wanted. In some minimal installs, depending upon distribution, instead of the old ifconfig command, you're supposed to use the ip command. 

Anyway, if you want to keep using **//ifconfig//**:

<code>yum install net-tools</code>

[[https://tty1.net/blog/2010/ifconfig-ip-comparison_en.html|ifconfig vs ip]]

[[https://srobb.net/ip.html|ip cheat sheet]]

===== Limit number of kernels =====

Edit **/etc/yum.conf** to:

<code>installonly_limit=2</code>

===== Install VirtualBox Guest Additions =====

Before proceeding to guest additions installation, we need to install development tools:

<code>
yum groupinstall "Development Tools"
yum install kernel-devel
</code>

[[https://wiki.centos.org/HowTos/Virtualization/VirtualBox/CentOSguest|Reference]]


===== Install Gnome GUI on CentOS 7 =====

==== Install Gnome GUI ====

Install Gnome GUI by issuing the following command:

<code># yum groupinstall "GNOME Desktop" "Graphical Administration Tools"</code>

==== Enable GUI on system start up ====


In CentOS 7,  systemd uses ‘targets’ instead of runlevels; /etc/inittab file is no more used to change run levels. 
Issue the following command to enable the GUI on system start.

<code># ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target</code>


===== Security Policy during installation =====

Starting from CentOS 7, during installation, you will be presented with the //Security Policy// dialog.

The Security Policy spoke allows you to configure the installed system following restrictions and recommendations (compliance policies) defined by the Security Content Automation Protocol (SCAP) standard. This functionality is provided by an add-on and has been added in Red Hat Enterprise Linux 7.2.

**IMPORTANT**

Applying a security policy is not necessary on all systems. This screen should only be used when a specific policy is mandated by your organization rules or governemnt regulations.

Ref: [[https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/sect-security-policy-x86.html|RHEL 7 Installation Guide]]


===== Firewall management (firewall-cmd) =====

[[https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7|reference]]

The firewalld daemon manages groups of rules using entities called **zones**. Network interfaces are assigned a zone to dictate the behavior that the firewall should allow.

NOTE: If not explicity specified with the //permanent// parameter, all changes are temporary.


List all active zones and associated NICs:

  firewall-cmd --get-active-zones

Print out zones's configuration:

  firewall-cmd --list-all

Permanently add a known service ( ie: iscsi-target ) to public zone:

  firewall-cmd --zone=public --add-service=iscsi-target --permanent
  firewall-cmd --reload

Get a list of the available zones:

  firewall-cmd --get-zones

Get a list of the available services:

  firewall-cmd --get-services

List all enabled services:

  firewall-cmd --zone=public --list-services

Permanently remove a known service ( ie: iscsi-target ) from public zone:

  firewall-cmd --zone=public --remove-service=iscsi-target --permanent
  firewall-cmd --reload

List only permanently enabled services:

  firewall-cmd --zone=public --permanent --list-services

Enable TCP access to port 5000:

  firewall-cmd --zone=public --add-port=5000/tcp
  firewall-cmd --reload

