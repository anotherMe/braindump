
## PSQLException: FATAL: sorry, too many clients already

Application ( JavaEE on Tomcat container using JDBC ) signals aforementioned error. But querying the DB there seem to be no pending connections:

  SELECT * FROM pg_stat_activity;

SSHing on the DB server and running a:

  # ps aux | grep postgres

though, shows a lot of processes.

### Solution

To kill all pending connections, just restart Postgres. 

To permanently resolve the issue, check your application to make sure all open connections get properly closed after use.

