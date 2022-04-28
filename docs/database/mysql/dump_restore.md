
# Dump

## Restoring dump with blobs

Trying to restore of a dump containing long lines and/or blobs, got error `MySQL Error 1153 - Got a packet bigger than 'max_allowed_packet' bytes`.

As per [this Stackoverflow post](https://stackoverflow.com/questions/93128/mysql-error-1153-got-a-packet-bigger-than-max-allowed-packet-bytes), I had to change some system variables on the database:

```sql
set global net_buffer_length=1000000; 
set global max_allowed_packet=1000000000;
```

