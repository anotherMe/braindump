

### JPA Enhancing without persistence.xml (almost)

Per evitare di creare e mantenere lunghissimi file `persistence.xml`, abbiamo adottato un apposito plugin di Maven, che ci consente di effettuare l'enhance delle classi entità in maniera dinamica

- modificato il `pom.xml`, aggiungendo il plugin **openjpa-maven-plugin** e la relativa configurazione dove specifichiamo anche le classi da includere o escludere:

    ```xml
    <plugin>
        <groupId>org.apache.openjpa</groupId>
        <artifactId>openjpa-maven-plugin</artifactId>
        <version>2.4.0</version>
        <configuration>
            <includes>**/entities/*.class</includes>
            <includes>**/entities/**/*.class</includes>
            <excludes>**/entities/XML*.class</excludes>
            <excludes>**/entities/**/XML*.class</excludes>
        </configuration>
        <executions>
            <execution>
                <id>enhancer</id>
                <phase>process-classes</phase>
                <goals>
                    <goal>enhance</goal>
                </goals>
            </execution>
        </executions>
        <dependencies>
            <dependency>
                <groupId>org.apache.openjpa</groupId>
                <artifactId>openjpa</artifactId>
                <version>2.4.0</version>
            </dependency>
        </dependencies>
    </plugin>
    ```


- aggiunto il file `resources\META-INF\persistence.xml`, che include una persistence unit di default ( ed eventualmente la PU che fa riferimento a *sisenv* ):

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <persistence xmlns="http://java.sun.com/xml/ns/persistence" version="2.0">
        <persistence-unit name="standard" transaction-type="RESOURCE_LOCAL">
            <properties>
                <property name="openjpa.jdbc.DBDictionary" value="mysql"/>
                <property name="openjpa.DataCache" value="false"/>
                <property name="openjpa.QueryCache" value="false"/>
            </properties>
        </persistence-unit>
    </persistence>
    ```


- modificata la classe `ReCargoWeb/src/main/java/it/sisnet/seven/cargo/TenantManager.java` per aggiungere un EM che faccia riferimento alla persistence unit *data*:

    ```java
    static {

        Reflections reflections = new Reflections(PACKAGE_PREFIX);
        Set<Class<?>> annotated = reflections.getTypesAnnotatedWith(Entity.class);
        classNames = annotated.stream().map(p -> p.getName())
                .filter( p -> p.startsWith("it.sisnet.") && p.contains(".entities"))
                .filter(p->!p.contains("osgi"))
                .collect(Collectors.toList());
    }
    ```

