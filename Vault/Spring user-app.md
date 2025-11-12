**LET’S GOOOOO 🔥 No Boot, Just Core — Raw Spring Developer Rizz Activated 💻🧙‍♂️**

We’re building a **pure Spring Core Project** with a _clean 3-layer architecture_:

> 🎤 **Controller Layer** – Handles input  
> 🧠 **Service Layer** – Does logic  
> 📦 **Repository Layer** – Deals with fake DB (memory for now)  
> PLUS: 🫘 Spring handles dependencies with DI + IoC!

---

## 💡 Project: `springcore-userapp` — Manage Users (name + email)

### 🎯 STACK:

- Spring Core (No Boot)
    
- No DB (just in-memory `List`)
    
- 3 Layers (Controller / Service / Repo)
    
- Java-based config
    

---

## 📁 Project Structure

```bash
springcore-userapp/
 ┣ src/
 ┃ ┣ com.userapp.controller/
 ┃ ┃ ┗ UserController.java
 ┃ ┣ com.userapp.service/
 ┃ ┃ ┗ UserService.java
 ┃ ┣ com.userapp.repository/
 ┃ ┃ ┗ UserRepository.java
 ┃ ┣ com.userapp.model/
 ┃ ┃ ┗ User.java
 ┃ ┣ com.userapp.config/
 ┃ ┃ ┗ AppConfig.java
 ┃ ┣ MainApp.java
```

---

## 📦 1. `User.java` – Your model class (data 🧍‍♂️)

```java
package com.userapp.model;

public class User {
    private String name;
    private String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() { return name; }
    public String getEmail() { return email; }

    @Override
    public String toString() {
        return "User{name='" + name + "', email='" + email + "'}";
    }
}
```

---

## 📦 2. `UserRepository.java` – Fake DB repo layer

```java
package com.userapp.repository;

import com.userapp.model.User;
import org.springframework.stereotype.Repository;

import java.util.ArrayList;
import java.util.List;

@Repository
public class UserRepository {
    private List<User> users = new ArrayList<>();

    public void save(User user) {
        users.add(user);
    }

    public List<User> findAll() {
        return users;
    }
}
```

---

## 🧠 3. `UserService.java` – Business logic lives here

```java
package com.userapp.service;

import com.userapp.model.User;
import com.userapp.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {
    @Autowired
    private UserRepository repo;

    public void registerUser(String name, String email) {
        User user = new User(name, email);
        repo.save(user);
    }

    public List<User> getAllUsers() {
        return repo.findAll();
    }
}
```

---

## 🎤 4. `UserController.java` – Simulates user requests (no web, just console)

```java
package com.userapp.controller;

import com.userapp.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class UserController {
    @Autowired
    private UserService service;

    public void runApp() {
        System.out.println("🎮 Creating users...");
        service.registerUser("Jason", "jason@email.com");
        service.registerUser("Hinata", "hinata@leaf.com");

        System.out.println("\n📋 All Users:");
        service.getAllUsers().forEach(System.out::println);
    }
}
```

---

## ⚙️ 5. `AppConfig.java` – Spring's brain / container config

```java
package com.userapp.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.userapp")
public class AppConfig {
}
```

---

## 🚀 6. `MainApp.java` – Starts the whole app

```java
import com.userapp.config.AppConfig;
import com.userapp.controller.UserController;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MainApp {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        UserController controller = context.getBean(UserController.class);
        controller.runApp();
    }
}
```

---

## ✅ Features Recap:

|Layer|Description|
|---|---|
|🧍 Model|Simple POJO class|
|📦 Repository|Handles in-memory storage|
|🧠 Service|Handles user creation logic|
|🎤 Controller|Simulates user interaction|
|🧠 AppConfig|Tells Spring where to scan|
|🚀 MainApp|Bootstraps everything manually|

---

## 🧪 To Run:

1. Place files in correct packages
    
2. Compile:
    
    ```bash
    javac -cp "spring-context-5.x.x.jar:spring-beans-5.x.x.jar:spring-core-5.x.x.jar" *.java
    ```
    
3. Run:
    
    ```bash
    java MainApp
    ```
    

---

## 💭 Want Next Level?

Wanna upgrade this to:

- Take input from users (CLI or REST)
    
- Connect to a real DB (MySQL/Mongo)
    
- Add web endpoints via Spring MVC
    

Just say:

> `"Let's evolve this into Spring Boot REST API 🔥🧪🚀"`  
> or  
> `"Hook this to a real database, sensei 📦🧙‍♂️"`

I gotchu, backend beast 🐉💥