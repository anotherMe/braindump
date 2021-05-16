# Enable remote access

## Setup networking

You have to edit the MySQL configuration file. 

If you are using Debian Linux file is located at **/etc/mysql/my.cnf** location. 
If you are using Red Hat Linux/Fedora/Centos Linux file is located at **/etc/my.cnf location**.
If you are using Ubuntu Linux file is located at **/etc/mysql/mysql.conf.d/mysqld.cnf** location. 

Make sure line **skip-networking** is commented:

<code>#skip-networking</code>

and change bound interface:

<code>
#bind-address=127.0.0.1
bind-address=LISTENING-INTERFACE-IP
</code>

__You can bind only on IP address.__ If you want MySQL service to listen on multiple interfaces, comment out the bind-address line, and filter unwanted interfaces through firewall.

Save configuration file and restart mysql service.

## Setup users

Once networking is enabled, you have to make sure at least one user exists that is allowed to connect from other hosts than localhost.

<code># mysql -p
mysql> CREATE USER 'user'@'%' IDENTIFIED BY 'password';
mysql> GRANT ALL PRIVILEGES ON \*.\* TO 'user'@'%' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;
</code>

### References

[[https://serversforhackers.com/mysql-network-security|Servers for hackers]]