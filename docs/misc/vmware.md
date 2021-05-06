
# VMWare

**NOTA**: pagina di riordinare

## Check filesystem
[[https://pubs.vmware.com/vsphere-55/index.jsp?topic=%2Fcom.vmware.vsphere.troubleshooting.doc%2FGUID-6F991DB5-9AF0-4F9F-809C-B82D3EED7DAF.html|source]]

Obtain the **Device name** and **partition number** of the device that backs the VMFS datastore that you need to check:

  # esxcli storage vmfs extent list

	
Check for VMFS errors on partition ( use DEVICENAME:PARTITIONNUMBER ). Example:

  # voma -m vmfs -f check -d t10.945445000000000065F8606B0323C1F871DAAF43C4C9490A:1

**NOTE**: Make sure that the VMFS datastore you analyze does not span multiple extents. You can run VOMA only against a single-extent datastore.

## How to stop a file copy which is started by vSphere client

(Applies to VMWare ESXi v5.x)

  # /sbin/services.sh restart

# ESXi

**Note**: All following commands refer to ESXi **version 5.x**.


## Common monitoring tasks

Top :

  ~ # esxtop

Get a list of running virtual machines:
  
  ~ # esxcli vm process list
  

## esxcli

List all commands tree:

  ~ # esxcli esxcli command list


List all VMs:

  ~ # esxcli vm process list


## Restart services

  ~ # services.sh restart


## Troubleshooting

### VM shutdown

Get a list of running virtual machines:

  ~ # esxcli vm process list

Power off the virtual machine from the list by running this command:

  ~ # esxcli vm process kill --type= [soft,hard,force] --world-id= WorldNumber

### ESXi stuck on running usbarbitrator start

It happened from time to time, when performing a services restart, that the ESXi hangs on the //running usbarbitrator start// step. To resolve, just open another SSH shell and issue:

  ~ # chkconfig usbarbitrator off

and then stop the service:

  ~ # service usbarbitrator stop



### Manuals

* [[https://pubs.vmware.com/vsphere-51/topic/com.vmware.ICbase/PDF/vsphere-esxi-vcenter-server-51-command-line-interface-solutions-and-examples-guide.pdf|vSphere Command-Line Interface - Concepts and Examples (ESXi 5.1)]]

* [[https://vdc-download.vmware.com/vmwb-repository/dcr-public/37dc6c55-7dc3-444b-973e-9290ffad06ab/1e788ab5-854b-409f-ad54-3305085674f4/vsphere-esxi-vcenter-server-55-command-line-interface-concepts-examples-guide.pdf|vSphere Command-Line Interface - Concepts and Examples (ESXi 5.5 update 1)]]


### References

* [[https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2012964|Performing common virtual machine-related tasks with command-line utilities (2012964)]]

* [[https://communities.vmware.com/docs/DOC-31025|Quick Tutorial for vim-cmd commands]]

* [[http://www.doublecloud.org/2013/11/vmware-esxi-vim-cmd-command-a-quick-tutorial|VMware ESXi vim-cmd Command: A Quick Tutorial]]

* [[http://www.doublecloud.org/2013/12/powerful-hacks-with-esxi-vim-cmd-command-together-with-shell-commands|Powerful Hacks With ESXi vim-cmd]]

* [[https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2032076|Location of ESXi 5.1 and 5.5 log files]]
