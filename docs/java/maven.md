
# Cookbook

## List the goals of a specific phase

Maven provides a command to list the goals that will be executed for a specific phase.

For example, to list the goals for the *package* phase:

  mvn help:describe -Dcmd=package

For reference, see the [Maven Help Plugin](https://maven.apache.org/plugins/maven-help-plugin/)


## Search and replace of strings using Velocity

( [Stackoverflow](https://stackoverflow.com/questions/2196394/full-search-and-replace-of-strings-in-source-files-when-copying-resources) )


## Compiling Sources Using A Different JDK
( [reference](https://maven.apache.org/plugins/maven-compiler-plugin/examples/compile-using-different-jdk.html) )

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <verbose>true</verbose>
        <fork>true</fork>
        <executable>${JAVA_11_HOME}/bin/javac</executable>
        <compilerVersion>11</compilerVersion>
    </configuration>
</plugin>
```

Dove la variabile **JAVA_11_HOME** deve essere definita nel file `settings.xml` ( su Window$, lo trovi sul percorso `C:\Users\IL_TUO_UTENTE\.m2\` ):

```xml
<settings>

    ...

    <profiles>
        <profile>
            <id>compiler</id>
            <properties>
                <JAVA_11_HOME>C:\opt\jdk-11</JAVA_11_HOME>
            </properties>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>compiler</activeProfile>
    </activeProfiles>

</settings>
```
