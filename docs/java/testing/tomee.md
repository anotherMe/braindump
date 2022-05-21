
# TomEE testing

## Testing with an embedded EJB container

This is an incomplete example, after the container has been started, you should register your beans, datasources, etc ...

Here we are using JUnit4.

```java
import org.junit.*;

import javax.ejb.embeddable.EJBContainer;
import javax.naming.Context;

import static org.junit.Assert.assertEquals;

public class EjbTestingPocTest {

    private static Context  ctx;
    private static EJBContainer ejbContainer;

    @BeforeClass
    public static void setUp() {
        ejbContainer = EJBContainer.createEJBContainer();
        System.out.println("Opening the container" );
        ctx = ejbContainer.getContext();
    }

    @AfterClass
    public static void tearDown() {
        ejbContainer.close();
        System.out.println("Closing the container" );
    }

    @Test
    public void simple() {
        assertEquals(1, 1);
    }
}
```


To use this approach, that is to use the javax.ejb.embeddable.EJBContainer API, you have to provided an implementation. This could be an example pom.xml:

```xml
<dependency>
    <groupId>org.apache.tomee</groupId>
    <artifactId>tomee-embedded</artifactId>
    <version>8.0.8</version>
    <scope>test</scope>
</dependency>
```

