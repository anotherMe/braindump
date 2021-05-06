
# Shell reference

List all databases:

  mysql> show databases;

Connect to specific database:

  mysql> use [DATABASE NAME];

List tables in db:

  mysql> show tables;

Show users:

  mysql> select host, user from mysql.user;


Create new __local__ user:

  mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
  mysql> GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'localhost';
  mysql> FLUSH PRIVILEGES;


### References

[[https://www.pantz.org/software/mysql/mysqlcommands.html|Pantz.org]]