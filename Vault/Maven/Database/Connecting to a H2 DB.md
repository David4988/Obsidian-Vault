- its the _go-to_ in memory DB

```java 
public class DatabaseApplication implements CommandLineRunner {  
  
    public final DataSource dataSource;  
  
    public DatabaseApplication(DataSource dataSource) {  
       this.dataSource = dataSource;  
    }  
  
    public static void main(String[] args) {  
       SpringApplication.run(DatabaseApplication.class, args);  
  
    }  
  
    @Override  
    public void run(String... args) {  
       log.info("DataSource: "+ dataSource.toString());  
       final JdbcTemplate restTemplate = new JdbcTemplate(dataSource);  
       restTemplate.execute("select 1");  
    }  
  
}
```

- **Here**, 

### 1. Injecting `dataSource` Object:

- We ***use constructor-based Dependency Injection*** to inject the `DataSource` into the `DatabaseApplication` class
```java
public final DataSource dataSource; //Injected into the class

public DatabaseApplication(DataSource dataSource) {  
       this.dataSource = dataSource;  
}
```

### 2. Logging the Info:

- Then, we are logging the info from the `dataSource` object to the *Command line*

```java
log.info("DataSource: "+ dataSource.toString());  
```

- Creating a **`JdbcTemplate`** object — this is a helper class from **Spring JDBC**  and injecting the `dataSource` object
- So, `JDBC` knows **how to connect to the DB**

```java
final JdbcTemplate restTemplate = new JdbcTemplate(dataSource);  
```

- Then we use the `restTemplate` object to *query our Database*
- Then we send a dummy query - `"select 1"` to check if **the database is alive**

```java
restTemplate.execute("select 1");  
```

- **Finally, the overall `run` method:**

```java
@Override  
    public void run(String... args) {  
       log.info("DataSource: "+ dataSource.toString());  
       final JdbcTemplate restTemplate = new JdbcTemplate(dataSource);  
       restTemplate.execute("select 1");  
    }  
```

---
- If we run the `databaseApplication` class, we get this output:
```bash
HikariPool-1 - Added connection conn0: url=jdbc:h2:mem:bf20fda0-acc1-4cc8-b9f1-ca1f6cacc7e3 user=SA
HikariPool-1 - Start completed.
HikariPool-1 - Shutdown initiated...
HikariPool-1 - Shutdown completed.
```

- here, even when we aren't giving it any `connection url` or the `user` details, `JDBC` auto configures it

- Spring Boot auto-configures a **temporary in-memory H2 database** when no data source is explicitly defined.  
- It assigns a random DB like:

```bash
jdbc:h2:mem:<random-id>
```

Uses default creds:

```properties
user=SA password= (empty)
```


Also, we can use the `application.properties` file to give a custom `database-id` `username` and `password`

```properties
spring.datasource.url=jdbc:h2:mem:testdb  
spring.datasource.driverClassName=org.h2.Driver  
spring.datasource.username=sa  
spring.datasource.password= password
```