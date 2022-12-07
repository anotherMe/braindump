
## Enable query logging

In file `./apache-tomee/conf/system.properties`:

```ini
openjpa.Log = DefaultLevel=TRACE, SQL=TRACE, Query=TRACE
openjpa.ConnectionFactoryProperties = printParameters=true
```

