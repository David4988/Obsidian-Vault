- If we want to get a Config from the `application.properties`  file, we use the 
`@ConfigurationProperties` annotation.

- `@ConfigurationProperties` annotation take an argument called `prefix` to identify the given **key** in the `application.properties` file

In `PizzaConfig.java`,
```java
@Configuration
@ConfigurationProperties(prefix = "pizza")
@AllArgsConstructor  
@NoArgsConstructor  
@Data // All getters/setters are already implemented by using Lombok  
public class PizzaConfig {  
    private String sauce;  
    private String topping;  
    private String crust;  
}
```

In `application.properties` file,
```properties
pizza.sauce=bbq
pizza.topping=chicken
pizza.crust=stuffed
```

- the `pizza` in `pizza.sauce` is the prefix declared in `PizzaConfig.java`

`PizzaApplication.java`
```java
@SpringBootApplication  
@Log  
public class PizzaApplication implements CommandLineRunner {  
  
    private PizzaConfig pizzaConfig;  
  
    public PizzaApplication(PizzaConfig pizzaConfig) {  
       this.pizzaConfig = pizzaConfig;  
    }  
  
    public static void main(String[] args) {  
       SpringApplication.run(PizzaApplication.class, args);  
    }  
  
    @Override  
    public void run(final String... args) {  
       log.info(  
             String.format("I want a %s crust pizza, with %s and %s sauce",  
                   pizzaConfig.getCrust(),  
                   pizzaConfig.getTopping(),  
                   pizzaConfig.getSauce()  
             ));  
    }  
}
```
