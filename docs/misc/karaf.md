

Edit `etc\user.properties` to enable *karaf* user:

```ini
karaf = karaf,_g_:admingroup
_g_\:admingroup = group,admin,manager,viewer,systembundles,ssh
```



Edit `etc\org.apache.karaf.management.cfg` to ???:

