
# Using socat-container to expose container ports

Given:

- MYCONTAINER - the container you want to connect to
- MYNETWORK - the docker network the container is running in ( you may omit the *network* parameter if the container is running on the default docker network )
- PORT - the port you want to reach from the outside
- EXTPORT - the port you'll use to reach through

you may expose port PORT of MYCONTAINER:

```bash
docker run --publish EXTPORT:PORT --network MYNETWORK --link MYCONTAINER:target alpine/socat tcp-listen:PORT,fork,reuseaddr tcp-connect:target:PORT
```


# Reclaim some space

Note: this two commands may seem a little bit disruptive ( we're trying to remove ALL the containers and ALL the images ), but docker will delete only containers and images that aren't currently in use.

```bash
docker rm $(docker ps -qa)
```

```bash
docker rmi $(docker images -q)
```

# JMX remote connection to Apache Karaf container

You have to provide a username and a password to access the JMX layer. The JMX layer uses the security framework, and so, by default, it uses the users defined in `etc/users.properties`.

Make sure that at least one user is enabled ( here the default *karaf* user ):

```
karaf = karaf,_g_:admingroup
_g_\:admingroup = group,admin,manager,viewer,systembundles,ssh
```


Make Karaf JMX listen to the [catch-all IP address](https://en.wikipedia.org/wiki/0.0.0.0). You do that by modifying the file `etc/org.apache.karaf.management.cfg`:


```
#
# Port number for RMI registry connection
#
rmiRegistryPort = 1099

#
# Host for RMI registry
#
#rmiRegistryHost = 127.0.0.1
rmiRegistryHost = 0.0.0.0

#
# Port number for RMI connector server connection
#
rmiServerPort = 44444

#
# Host for RMI connector server
#
#rmiServerHost = 127.0.0.1
rmiServerHost = 0.0.0.0 
```

If you like, you can also change the ports the JMX server listens to. In any case, **make sure that the registry port and the server port are exposed from the container**.


Supposing that the IP of the docker host is 172.16.20.105, you should now be able to remotely connect to your the running container using the JMX URL:

```
service:jmx:rmi://172.16.20.105:44444/jndi/rmi://172.16.20.105:1099/karaf-root
```


### References 

[Apache Karaf Container 4.x - Documentation](https://karaf.apache.org/manual/latest/#_monitoring_and_management_using_jmx)