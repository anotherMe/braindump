====== Temporary tables ======

Temporary tables exist in a special schema, so a schema name cannot be given when creating a temporary table.

Temporary tables are automatically dropped at the end of a session, or optionally at the end of the current transaction (see ON COMMIT below). 

Existing permanent tables with the same name are not visible to the current session while the temporary table exists, unless they are referenced with schema-qualified names. 

Any indexes created on a temporary table are automatically temporary as well.

The autovacuum daemon cannot access and therefore cannot vacuum or analyze temporary tables. For this reason, appropriate vacuum and analyze operations should be performed via session SQL commands. For example, if a temporary table is going to be used in complex queries, it is wise to run ANALYZE on the temporary table after it is populated.

Foreign key constraints cannot be defined between temporary tables and permanent tables.

===== ON COMMIT =====

The behavior of temporary tables at the end of a transaction block can be controlled using ON COMMIT. The three options are:

==== PRESERVE ROWS ====

No special action is taken at the ends of transactions. This is the default behavior.

==== DELETE ROWS ====

All rows in the temporary table will be deleted at the end of each transaction block. Essentially, an automatic TRUNCATE is done at each commit.

==== DROP ====

The temporary table will be dropped at the end of the current transaction block.

===== TABLESPACE =====

The tablespace is the name of the tablespace in which the new table is to be created. If not specified, default_tablespace is consulted, or temp_tablespaces if the table is temporary.

===== Compatibility =====

The standard's distinction between global and local temporary tables is not in PostgreSQL, since that distinction depends on the concept of modules, which PostgreSQL does not have. For compatibility's sake, PostgreSQL will accept the GLOBAL and LOCAL keywords in a temporary table declaration, but they have no effect.

The ON COMMIT clause for temporary tables also resembles the SQL standard, but has some differences. If the ON COMMIT clause is omitted, SQL specifies that the default behavior is ON COMMIT DELETE ROWS. However, the default behavior in PostgreSQL is ON COMMIT PRESERVE ROWS. The ON COMMIT DROP option does not exist in SQL.