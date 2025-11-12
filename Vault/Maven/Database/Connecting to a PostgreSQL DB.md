[[Connecting to a H2 DB]]

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

- in `application.properties` file

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres  
spring.datasource.username=postgres  
spring.datasource.password=changemeinprod!  
spring.datasource.driver-class-name=org.postgresql.Driver

spring.sql.init.mode=always
```

- we also need Docker to use `postgreSQL` ,

- in the `docker-compose.yml` file,

```yml
services:  
  db:  
    image: postgres  
    volumes:  
      - ./gdata:/var/lib/postgresql/data/  
    environment:  
      POSTGRES_USER: postgres  
      POSTGRES_PASSWORD: changemeinprod!  
      POSTGRES_DB: postgres  
    ports:  
      - "5432:5432"
```

- Creating DB Schema in `schema.sql`

```sql
DROP TABLE IF EXISTS "widgets";  
  
DROP SEQUENCE IF EXISTS "widgets_id_seq";  
  
CREATE SEQUENCE "widgets_id_seq" INCREMENT 1 MINVALUE 1 MAXVALUE 9223372036854775807 CACHE 1;  
  
CREATE TABLE "widgets" (  
    "id" bigint DEFAULT nextval('widgets_id_seq') NOT NULL,  
    "name" text,  
    "purpose" text,  
    CONSTRAINT "widgets_pkey" PRIMARY KEY ("id")  
);
```

- Adding data in `data.sql`

```sql
INSERT INTO widgets (id, name, purpose) VALUES  
(1, 'widget1', 'used for testing purposes'),  
(2, 'widget2', 'Designed for entertainment'),  
(3, 'widget3', 'Enhances Productivity'),  
(4, 'widget4', 'Perfect for Outdoor Activities'),  
(5, 'widget5', 'Improves Health');
```
