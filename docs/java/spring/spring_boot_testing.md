
# Spring Boot testing

## Application context creation

When testing a Spring Boot application, you can create the **Application Context** using the **@SpringBootTest** annotation:

```java
@SpringBootTest
class MyClassTest {
}
```

## Override default Spring-Boot application.properties settings in Junit Test

### Using @TestPropertySource annotation

```java
@SpringBootTest
@TestPropertySource(locations="classpath:test.properties")
class MyClassTest {
}
```

**NOTE** This works only with *.properties* files, not with *.yml*

### Using profiles

```java
@SpringBootTest
@ActiveProfiles("test") 
@Testcontainers
class MyClassTest {
}
```

Just create the file `src/test/resources/application-test.yml`. Every property defined in this file will overwrite the ones defined in `src/java/resources/application.yml`

