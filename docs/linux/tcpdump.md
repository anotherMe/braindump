
# tcpdump

## Capturing

Capture traffic flowing through interface //**ens34**//, recording the whole packet (65535 bytes maximum) instead of just a few bytes, and write the output in raw format to a file named //dump//:

  # tcpdump -i ens34 -w dump -s 65535

Capture traffic flowing through all interfaces:

  # tcpdump -i any -w dump

Note that, when running with the "-i any" option, tcpdump cannot put the NIC in promiscous mode.

## Filtering

Capture traffic with destination port //**25**// on interface //**ens34**//:

  # tcpdump -i ens34 dst port 25


## Post-processing

It's possible to read a file and do further processing on it.

### Split PCAP file

Split too big PCAP file in smaller chunks:

  tcpdump -r input_file.pcap -w output -C 100

In the above example, data is read from //input_file.pcap// and written back to a series of //outputXXX// files, each on sized about 100 MB.


## tcpdump and iptables

When setting up iptables rules, you then have to keep in mind that tcpdump is the first software found after the wire (and the NIC, if you will) on the way IN, and the last one on the way OUT.

<code>

------
|wire| -> NIC -> tcpdump -> netfilter/iptables
------
----------
|iptables| -> tcpdump -> NIC -> wire
----------
</code>

That is to say, tcpdump will show all ingoing packets before they eventually get blocked by iptables. On the other hand, if you block some outgoing packet, you will not be longer able to see it in tcpdump.
