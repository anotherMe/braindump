

# MySQL data source with Apache Commons DBCP

Below is an example of a "manual" creation of the EntityManager, useful when testing container managed EM where the container is not available or too expensive / too complex to create during tests:

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

// list of classes that need to be enhanced
EntityManagerFactory emf = new JpaEntityManagerFactory(new Class[] {

		A3Carico.class,
		A3CaricoDet.class,
		A3CaricoDetCancellate.class,

}).getEntityManagerFactory("TEST", dataSource);

EntityManager em = emf.createEntityManager();
```


# MySQL data source with MySQL Connector

Pom dependencies:

```xml
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.29</version>
	<scope>test</scope>
</dependency>
```


```java

import com.mysql.cj.jdbc.MysqlDataSource;
import it.sisnet.seven.osgi.scambio.entities.processi.MessaggiApi;
import it.sisnet.seven.osgi.scambio.jpa.JpaEntityManagerFactory;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;

MysqlDataSource dataSource = new MysqlDataSource();

dataSource.setUser("MYUSER");
dataSource.setPassword("MYPASSWORD");
dataSource.setUrl("jdbc:mysql://HOST:PORT/DATABASE");

// list of classes that need to be enhanced
EntityManagerFactory emf = new JpaEntityManagerFactory(new Class[] {

		MessaggiApi.class

}).getEntityManagerFactory("TEST", dataSource);

EntityManager em = emf.createEntityManager();

```


# H2 data source

```java
import org.h2.jdbcx.JdbcDataSource;

JdbcDataSource ds = new JdbcDataSource();
ds.setURL("jdbc:h2:˜/test");
ds.setUser("sa");
ds.setPassword("sa");

// list of classes that need to be enhanced
EntityManagerFactory emf = new JpaEntityManagerFactory(new Class[] {

		MessaggiApi.class

}).getEntityManagerFactory("TEST", ds);

EntityManager em = emf.createEntityManager();

```