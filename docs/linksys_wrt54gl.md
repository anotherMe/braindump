====== Linksys WRT54GL ======

===== From from stock firmware image to OpenWRT =====

You can find detailed instructions on [[https://wiki.openwrt.org/toh/linksys/wrt54g#installing_openwrt|Installing OpenWrt]] page.

===== From OpenWRT to stock firmware image =====

SSH into the WRT54GL router, then proceed to download the firmware:

<code>
cd /tmp
wget http://www.example.org/original_firmware.bin
</code>

We now need to transform the original bin image into a trx image ( we just have 
to strip the first 32 bytes ):

<code>
dd bs=32 skip=1 if=original.bin of=original.trx
</code>

Finally, flash the image:

<code>
mtd -r write /tmp/original.trx linux
</code>


**NOTE**: as of 25/08/2016 I've downloaded the firmware from [[http://cache-www.belkin.com/support/dl/FW_WRT54GL_4.30.18.006_US_20160108.bin|this]] page.

Reference: [[https://wiki.openwrt.org/doc/howto/generic.uninstall|OpenWRT wiki]]

===== OpenWRT reset using failsafe =====

==== Get started ====

* Power off the router
* Unplug the WAN port and connect your PC connected to one of the LAN ports
* Set your computer's IP to 192.168.1.2, subnet 255.255.255.0

==== Boot in failsafe mode ====

* Power on the router
* As soon as this blink pattern is seen, press the reset button rapidly
* The SYS LED will change to faster blink pattern ( and keep blinking ), indicating the router is now in failsafe mode

==== Telnet into the router ====

* telnet into the router ( which should now have 192.168.1.1 )
* reset:

<code>
mount_root
mtd -r erase rootfs_data
reboot -f
</code>



==== Reset ====



Reference: [[https://support.rbtechvt.com/knowledgebase/article/View/61/0/how-to-clear-openwrt-config-back-to-factory-settings|RB Technologies]]