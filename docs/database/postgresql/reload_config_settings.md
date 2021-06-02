# How to reload config settings without restarting database

## Option 1: From the command-line shell

  su - postgres
  /usr/bin/pg_ctl reload


## Option 2: Using SQL

<code class="SQL">SELECT pg_reload_conf();</code>


[[http://www.heatware.net/databases/postgresql-reload-config-without-restarting/|source]]