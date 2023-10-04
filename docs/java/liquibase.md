
# Liquibase

## Runnning the Maven plugin

Create a new Maven run configuration for the **liquibase** plugin: 

```bash
compile liquibase:update -pl <MODULE_NAME> -f pom.xml
```

Here, we need to `compile` the project before running tha Maven goal.

Then edit the configuration in order to set the **Working directory** to the project base dir ( not the module's dir ). It's the `-pl` option that will tell Maven what *module* we are currently working on.


## Baseline a new database environment

To generate the `src/main/resources/config/liquibase/master.xml` file, from an already created database:

```bash
mvn compile liquibase:generateChangeLog -pl <MODULE_NAME> -f pom.xml
```

Then, to syncronize the Liquibase changelog tables:

```bash
mvn compile liquibase:changelogSync -pl <MODULE_NAME> -f pom.xml
```

( Note that you have to `compile` before you run the plugin )


Cloearly, to run the above commands, you need to have the Liquibase plugin configured in your `pom.xml`. For example:

```xml
<plugin>
                <groupId>org.liquibase</groupId>
                <artifactId>liquibase-maven-plugin</artifactId>
                <version>4.22.0</version>
                <configuration>
                    <outputChangeLogFile>${project.basedir}/src/main/resources/config/liquibase/master.xml
                    </outputChangeLogFile>
                    <changeLogFile>/config/liquibase/master.xml</changeLogFile>
                    <diffChangeLogFile>
                        ${project.basedir}/src/main/resources/config/liquibase/changelog/${maven.build.timestamp}_changelog.xml
                    </diffChangeLogFile>
                    <driver>org.postgresql.Driver</driver>
                    <url>jdbc:postgresql://localhost:5432/my_database</url>
                    <defaultSchemaName>my_schema</defaultSchemaName>
                    <username>my_user_name</username>
                    <password>my_password</password>
                    <verbose>true</verbose>
                    <logging>debug</logging>
                    <contexts>!test</contexts>
                </configuration>
                <dependencies>
                </dependencies>
            </plugin>
```

### References

- [Maven changelogSync](https://docs.liquibase.com/tools-integrations/maven/commands/maven-changelogsync.html)
- [Maven generateChangeLog](https://docs.liquibase.com/tools-integrations/maven/commands/maven-generatechangelog.html)
- [Configuring Liquibase Attributes in your Maven POM File](https://docs.liquibase.com/tools-integrations/maven/maven-pom-file.html)