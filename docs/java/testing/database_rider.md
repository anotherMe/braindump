
# Good practeces

## Always include logging

In order to get meaningful messages when running the tests, remember to always include in your pom.xml the needed dependencies:

```xml
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.32</version>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.32</version>
            <scope>test</scope>
        </dependency>
```


# Troubleshooting

## Linkage error when using OpenJPA JDK8 to run the tests


There's something fucky when running OpenJPA and JDK 1.8. You could stumble on this error:

     407  riderDB  INFO   [main] openjpa.Runtime - Starting OpenJPA 2.4.0

    java.lang.LinkageError: loader (instance of  sun/misc/Launcher$AppClassLoader): attempted  duplicate class definition for name: "org/apache/openjpa/jdbc/identifier/DBIdentifier$DBIdentifierType"
    at java.lang.ClassLoader.defineClass1(Native Method)
        at java.lang.ClassLoader.defineClass(ClassLoader.java:756)
        at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:142)
        at java.net.URLClassLoader.defineClass(URLClassLoader.java:468)
        at java.net.URLClassLoader.access$100(URLClassLoader.java:74)
        at java.net.URLClassLoader$1.run(URLClassLoader.java:369)
        at java.net.URLClassLoader$1.run(URLClassLoader.java:363)
        at java.security.AccessController.doPrivileged(Native Method)



**Solution** was to modify the *run configuration* of the test, setting a more recent version of the JDK.


