
# Binary log files

**Problem**: You have a large amount of bin files in the MySQL data directory called “server-bin.n” or mysql-bin.00000n, eating up your server disk space.

## The purpose of MySQL Binary Log

The binary log has two important purposes:

  * **Data Recovery** : It may be used for data recovery operations. After a backup file has been restored, the events in the binary log that were recorded after the backup was made are re-executed. These events bring databases up to date from the point of the backup.

  * **High availability / replication** : The binary log is used on master replication servers as a record of the statements to be sent to slave servers. The master server sends the events contained in its binary log to its slaves, which execute those events to make the same data changes that were made on the master.

## Solution

You have two choices:

* disable binlogging
* purge / reset

If you ARE NOT replicating, you can disable binlogging.

If you ARE replicating, then you need to periodically RESET MASTER or PURGE MASTER LOGS. To do so, connect to mysql:

  # mysql -u root -p

then, issue __one__ of the following commands:

  mysql> RESET MASTER;
  mysql> PURGE BINARY LOGS TO 'mysql-bin.010';
  mysql> PURGE BINARY LOGS BEFORE '2008-04-02 22:46:26';


### References

[[https://www.cyberciti.biz/faq/what-is-mysql-binary-log/]]
[[https://dev.mysql.com/doc/refman/5.7/en/reset-master.html|MySQL manual - RESET MASTER Syntax]]
[[https://dev.mysql.com/doc/refman/5.7/en/purge-binary-logs.html|MySQL manual - PURGE BINARY LOGS Syntax]]