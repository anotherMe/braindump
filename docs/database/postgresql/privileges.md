# Manage privileges

You want to have it configured so only the hostdb_admin can create (and drop and alter) tables; the hostdb_mgr can read, insert, update and delete on all tables by default; and the hostdb_usr can only read all tables (and views).

As superuser //postgres//:

<code>
CREATE USER schma_admin WITH PASSWORD 'youwish';
CREATE USER schma_mgr   WITH PASSWORD 'youwish2';
CREATE USER schma_usr   WITH PASSWORD 'youwish3';
</code>


Grant each role to the next higher level, so all levels "inherit" at least the set of privileges from the next lower level (cascading):

<code>
GRANT schma_usr TO schma_mgr;
GRANT schma_mgr TO schma_admin;

CREATE DATABASE hostdb;
REVOKE ALL ON DATABASE hostdb FROM public;  -- see notes below!

GRANT CONNECT ON DATABASE hostdb TO schma_usr;  -- others inherit
</code>

  \connect hostdb  -- psql syntax

<code>
CREATE SCHEMA schma AUTHORIZATION schma_admin;

SET search_path = schma;  -- see notes

ALTER ROLE schma_admin IN DATABASE hostdb SET search_path = schma; -- not inherited
ALTER ROLE schma_mgr   IN DATABASE hostdb SET search_path = schma;
ALTER ROLE schma_usr   IN DATABASE hostdb SET search_path = schma;

GRANT USAGE  ON SCHEMA schma TO schma_usr;
GRANT CREATE ON SCHEMA schma TO schma_admin;

ALTER DEFAULT PRIVILEGES FOR ROLE schma_admin
GRANT SELECT                           ON TABLES TO schma_usr;  -- only read

ALTER DEFAULT PRIVILEGES FOR ROLE schma_admin
GRANT INSERT, UPDATE, DELETE, TRUNCATE ON TABLES TO schma_mgr;  -- + write, TRUNCATE optional

ALTER DEFAULT PRIVILEGES FOR ROLE schma_admin
GRANT USAGE, SELECT, UPDATE ON SEQUENCES TO schma_mgr;  -- SELECT, UPDATE are optional 
</code>

### Reference

[[http://dba.stackexchange.com/questions/117109/how-to-manage-default-privileges-for-users-on-a-database-vs-schema/117661#117661|SO]]


