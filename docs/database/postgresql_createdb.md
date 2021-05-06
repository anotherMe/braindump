## Create user

<code>
$ sudo su - postgres
$ psql
</code>

Then create user with LOGIN privilege:

  CREATE ROLE myuser LOGIN ;
or
  CREATE USER myuser;

Set a password :

  alter role myuser password 'password!';


## Create database

<code>
$ sudo su - postgres
$ psql
=# create database MYDATABASE;
</code>
