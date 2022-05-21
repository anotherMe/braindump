
# jlink & jdeps

**Goal**: creare una versione "leggera" del JRE che contenga le sole librerie necessarie.

Il JDK fornisce lo strumento **jdeps** per creare in maniera automatica l'elenco delle dipendenze, a partire ad esempio da un JAR:

```
C:\opt\jdk-11\bin\jdeps.exe target\ReAida-1.0.jar
```

e questo è un esempio (con omissis!) dell'output:

```
ReAida-1.0.jar -> java.base
ReAida-1.0.jar -> java.logging
ReAida-1.0.jar -> java.sql
ReAida-1.0.jar -> not found
   it.sisnet.seven.reaida                             -> com.google.common.base                             not found
   it.sisnet.seven.reaida                             -> it.sisnet.seven.reaida.handlers                    ReAida-1.0.jar
   it.sisnet.seven.reaida                             -> java.lang                                          java.base
   it.sisnet.seven.reaida                             -> org.apache.camel                                   not found
...
   it.sisnet.seven.reaida.controllers                 -> java.io                                            java.base
   it.sisnet.seven.reaida.controllers                 -> java.lang                                          java.base
   it.sisnet.seven.reaida.controllers                 -> java.lang.invoke                                   java.base
   it.sisnet.seven.reaida.controllers                 -> java.net                                           java.base
   it.sisnet.seven.reaida.controllers                 -> java.security                                      java.base
   it.sisnet.seven.reaida.controllers                 -> java.sql                                           java.sql
...
   org.springframework.boot.loader.jarmode            -> org.springframework.core.io.support                not found
   org.springframework.boot.loader.jarmode            -> org.springframework.util                           not found
   org.springframework.boot.loader.util               -> java.io                                            java.base
   org.springframework.boot.loader.util               -> java.lang                                          java.base
   org.springframework.boot.loader.util               -> java.util                                          java.base
```


Una volta che disponiamo dell'elenco dei moduli, possiamo creare una versione customizzata del JRE:

```
C:\opt\jdk-11\bin\jlink.exe --module-path C:\opt\jdk-11\jmods --add-modules java.base,java.sql,java.logging --output customjre
```

Con l'opzione *add-modules*, forniamo un elenco di moduli ricavato in precedenza. Mentre, con l'opzione *output*, indichiamo
la directory in cui andrà creato il JRE custom.


## References

- [DZone - Dockerizing With a Custom JRE](https://dzone.com/articles/dockerizing-with-a-custom-jre)
- [Baeldung - Guide to jlink](https://www.baeldung.com/jlink)
- [Java 11 modules list](https://docs.oracle.com/en/java/javase/11/docs/api/)


