
## SSH key-based authentication

Key-based authentication is the most secure of several modes of authentication usable with OpenSSH.

SSH can use either "RSA" (Rivest-Shamir-Adleman) or "DSA" ("Digital Signature Algorithm") keys, but RSA is the only recommended choice for new keys.

The **private key** is kept on the computer you log from, while the **public key** is stored on the .ssh/authorized_keys file on all the computers you want to log in to.

The creation of a set of RSA keys is done on the __client machine__:

  mkdir ~/.ssh
  chmod 700 ~/.ssh
  ssh-keygen -t rsa

Your public key is now available in the choosen folder ( ex: .ssh/id_rsa.pub )

Now you should safely transfer your public key on the server machine:

  ssh-copy-id <username>@<host>

### References

 * [[https://en.wikipedia.org/wiki/Public-key_cryptography|Wikipedia - Public key cryptography]]
 * [[https://help.ubuntu.com/community/SSH/OpenSSH/Keys|Ubuntu help - SSH/OpenSSH/Keys]]



## SSH key-based authentication on ESXi/ESX hosts

For ESXi 5.x, 6.0 and 6.5 the location of authorized_keys is: 

  /etc/ssh/keys-<username>/authorized_keys

More than one key can be stored in this file.

### References

[[https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1002866|VMWare Knowledge Base]]


## Enable SSH root login on Debian

The SSH root login on the Debian Linux is disabled by default. To enable SSH login for a root user on Debian Linux system you need to first configure SSH server. Open **/etc/ssh/sshd_config** and change the following line:

<code>
FROM:
PermitRootLogin without-password
TO:
PermitRootLogin yes
</code>

Once you made the above change restart your SSH server:

<code># /etc/init.d/ssh restart</code>

[[https://linuxconfig.org/enable-ssh-root-login-on-debian-linux-server|source]]

===== Troubleshooting =====

In case of problems, it can be useful trying to connect to your server increasing verbosity:

  ssh YOURUSER@YOUR.SERVER -vvv


===== Useful links =====

[[http://www.cyberciti.biz/tips/linux-unix-bsd-openssh-server-best-practices.html|OpenSSH Best Security Practices]]