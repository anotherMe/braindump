
# Apache Camel testing


## Overwrite configuration

Given this example `src/main/resources/application.yml`:

```yml
my_route:
  remote_dir_in: 'sftp://user@host:22/in_new?binary=true&disconnect=true&delete=true&delay=10000&maxMessagesPerPoll=5&useUserKnownHostsFile=false'
```


you can create a test configuration `src/test/resources/application-test.yml`:

```yml
my_route:
  remote_dir_in: 'direct:input1'
```

and then use this alternate configuration in your tests:

```java

@SpringBootTest
@ActiveProfiles("test") // this annotation activates the application-test.yml
public class GestoreG4CostaMockingTest {

```

One of the limits of this approach is that you may have your routes declared differently and not so easily overridable.



## Using AdviceWith

In case we cannot or want not to change routes through the `application-test.yml`, we can change them at runtime:

```java
@Test
public void testingWithAdviceWith() throws Exception {

    AdviceWith.adviceWith(context, "ReCargo_RicezioneEsito", a ->
            a.mockEndpoints("direct:input")
    );

    context.start();
```

we just look up every routes ( by its *ID* ) and then manipulate the endpoints.

In order to avoid that routes get started, then stopped and then started again, we annotate the test class with `@UseAdviceWith ` and
then we manually start the routes with `context.start()`.


## Testing single handler by mocking the exchange

This one seems so simple that I still can't believe it.

```java

import org.apache.camel.CamelContext;
import org.apache.camel.Exchange;
import org.apache.camel.impl.DefaultCamelContext;
import org.apache.camel.impl.DefaultExchange;

CamelContext ctx = new DefaultCamelContext();
Exchange ex = new DefaultExchange(ctx);

String someString = "hello";
ex.getIn().setHeader("myHeader", someString);

ex.getIn().setBody(SOME_FANCY_OBJECT);

MyFancyHandler fancy = new MyFancyHandler();
fancy.elabora(ex);
```