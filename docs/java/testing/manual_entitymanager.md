
Below is an example of a "manual" creation of the EntityManager, useful when testing container managed EM where the container is not available or too expensive during tests:

```java
BasicDataSource dataSource = new BasicDataSource();

dataSource.setDriverClassName("com.mysql.jdbc.Driver");
dataSource.setUsername("USERNAME");
dataSource.setPassword("PASSWORD");
dataSource.setUrl("jdbc:mysql://HOST:PORT/DATABASE");
dataSource.setMaxTotal(10);
dataSource.setMaxIdle(5);
dataSource.setInitialSize(5);
dataSource.setValidationQuery("SELECT 1");

EntityManagerFactory emf = new JpaEntityManagerFactory(new Class[] {

		A3Carico.class,
		A3CaricoDet.class,
		A3CaricoDetCancellate.class,

}).getEntityManagerFactory("TEST", dataSource);

EntityManager em = emf.createEntityManager();
```

