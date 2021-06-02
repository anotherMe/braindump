# Wireshark

## OSI model

| Wireshark capture  | capture unit  | OSI model (reverse order) |
|--------------------|---------------|---------------------------|
| Frame              | bits          | physical                  |
| Ethernet           | frames        | data link                 |
| IP                 | packets       | network                   |
| TCP                | segments      | transport                 |


## How to sniff traffic on remote machine

On Linux and OSX you can achieve this by running tcpdump ( on the remote machine ) over ssh and having wireshark listen ( on the local machine ) on the pipe.

Create a named pipe:

<code>$ mkfifo /tmp/remote</code>

Start wireshark from the command line

<code>$ wireshark -k -i /tmp/remote</code>

Run tcpdump over ssh on your remote machine and redirect the packets to the named pipe:

<code>$ ssh root@firewall "tcpdump -s 0 -U -n -w - -i eth0 not port 22" > /tmp/remote</code>

## Come installare tcpdump su OpenSuse 11.4

```bash
# wget http://download.opensuse.org/repositories/openSUSE:/11.4/standard/i586/tcpdump-4.1.1-4.1.i586.rpm
# yast2 -i tcpdump-4.1.1-4.1.i586.rpm
```


### References

- [Wireshark wiki - Capture setup](https://wiki.wireshark.org/CaptureSetup/Pipes)


