- To use Environment Variables instead of using config files, we make the **key** uppercase and add a `_` in the place of any delimiter like `.`.

- E.g. , in `application.properties` file we mention the **server port** as
```yaml
server.port = 8181
```

but if we want to mention port as an **environment variable** , 

```bash
D:\SpringBoot> SERVER_PORT=8282 ./mvnw spring-boot:run
```

we can also, export the env variables and then, start building the project

```bash
D:\SpringBoot> export SERVER=8383
D:\SpringBoot> ./mvnw spring-boot:run
```
then, the server will run on `port:8383`