
```sql
CREATE USER 'MY_USER'@'%' IDENTIFIED BY 'df98h234098h2f45870';
-- SET PASSWORD FOR 'MY_USER'@'%' = PASSWORD('df98h234098h2f45870');
GRANT Insert ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Select ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Show view ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT References ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Trigger ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Update ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Lock tables ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Execute ON MY_DATABASE.* TO 'MY_USER'@'%';
GRANT Delete ON MY_DATABASE.* TO 'MY_USER'@'%';
```