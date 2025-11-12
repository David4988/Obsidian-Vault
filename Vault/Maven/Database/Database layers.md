- Spring Database is stacked in **3 layers** 

```
🧑 You → 🌐 Controller → 💼 Service
→ 🎯 JPA / Hibernate
→ 🧵 JDBC
→ 🔌 JDBC Driver
→ 🛢️ Database (MySQL/Postgres/etc)
```

## 1. Database Driver - The DB Translator 📡

- Every `POSTGRESS` or `SQL` database creates a **Java Database Driver** (.jar) which helps you _manage the database with your code_

- 🧪 You declare this in your `pom.xml` or `build.gradle`.

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

## 2. Java Database Connectivity - The OG Warrior 🧱

> _"Back in my day, we wrote our SQL with our own hands 💪."_

- JDBC is the **lowest level API** for DB access in Java.

-  Uses SQL queries to communicate with DB

- Need to do all the Java object mappings by yourself

- You can use it directly, but it's verbose AF 💀

```java
Connection conn = DriverManager.getConnection(url, user, password);
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users");
ResultSet rs = stmt.executeQuery();
```

🧠 Spring uses JDBC under the hood — even Hibernate uses JDBC eventually!

## 3. Java Persistence Layer - The Fancy Samurai 🎎

> ✨ _"I don’t like writing SQL, I want magic."_

- Uses Java Objects and does all the SQL mappings for you

-  **JPA** is just a **specification**. It tells how Java should interact with databases through objects (ORM = Object Relational Mapping).
    
- Spring Boot uses **Spring Data JPA**, which wraps JPA with cool autoconfig ✨.
    
- Common implementations: **Hibernate**, **EclipseLink**.

```java
@Entity
public class User {
   @Id
   @GeneratedValue
   private Long id;

   private String username;
}
```

