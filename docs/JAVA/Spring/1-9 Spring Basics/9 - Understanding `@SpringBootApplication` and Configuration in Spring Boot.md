#spring #java
## `@SpringBootApplication` — What It Really Does

This annotation is **not just a label** — it's a shortcut for 3 core Spring annotations:

| Annotation              | Purpose |
|--------------------------|---------|
| `@Configuration`         | Marks the class as a **configuration class** — Spring looks here for bean definitions. |
| `@ComponentScan`         | Tells Spring to **scan for components (beans)** starting from this package and below. |
| `@EnableAutoConfiguration` | Enables **Spring Boot’s auto-configuration**, which provides sensible defaults and setups. |

> It’s the main entry point that wires everything up automatically.

---

## Auto-Configuration & Spring Boot Starters

### 🔄 Auto-Configuration

When your Spring Boot app starts, auto-configuration:
- **Guesses what you need** based on your dependencies.
- **Creates default beans/config** (e.g., DataSource, MVC, Jackson, etc.).
- Reduces the amount of setup code you need to write.

Example:  
If Spring detects `spring-boot-starter-web`, it will:
- Set up Spring MVC
- Start an embedded Tomcat server
- Configure Jackson for JSON
5432
---

### 🚀 Spring Boot Starters

Spring Boot **starters** are pre-packaged dependency sets for common features.

| Starter                | Purpose |
|------------------------|---------|
| `spring-boot-starter-web` | Web apps with REST, Spring MVC, embedded Tomcat |
| `spring-boot-starter-data-jpa` | JPA + Hibernate + DB drivers |
| `spring-boot-starter-test` | JUnit, Mockito, Spring Test |
| `spring-boot-starter-security` | Spring Security defaults |
| `spring-boot-starter-thymeleaf` | Thymeleaf templating engine |

> You choose what starter fits your use case — Spring boot handles the wiring.

---

## Configuration Files in Spring Boot

Spring Boot supports external configuration through:

- `application.properties`
- `application.yml`

> These files live under:  
> `src/main/resources/`

 Example: `.properties`

```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
```

Example: `.yml`
```yaml
server:
  port: 8082

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
```


✅ Why Use YAML?

- Cleaner syntax
- Supports nesting and reduces repetition
- More readable for complex configurations
---
## Environment-Specific Config

Spring Boot can load different config files for different environments:
```bash
application.properties
application-dev.properties
application-test.properties
```

Set Profile using :
	`-Dspring.profiles.active=test`

You can also add test-specific config under:
	`src/test/resources/application.properties`

Example:
- Use in-memory DB (like H2) during tests
- Avoid overwriting production DBs

We can find all the properties we can edit. FIND [here](https://docs.spring.io/spring-boot/appendix/application-properties/index.html) 

---
# Using Environment Variables in Spring Boot

In real-world projects, you often **don’t want to hardcode sensitive or environment-specific values** (like passwords, DB URLs, or secrets) inside `application.properties`.

Instead, use **environment variables**.

---

## ✅ Why Use Environment Variables?

| Reason                  | Explanation                                                              |
| ----------------------- | ------------------------------------------------------------------------ |
| 🔒 Security             | Keeps credentials out of source code.                                    |
| 🔁 Flexibility          | Easily switch configs between dev, staging, prod.                        |
| ⚙️ DevOps/Cloud Support | Platforms like Docker, Kubernetes, AWS, etc., expect env-based config.   |
| 🧪 Test Isolation       | Use in-memory/test-specific values without changing actual config files. |

---

## 🔄 How Spring Boot Resolves Configuration

Spring Boot follows a **priority order** to resolve config values. Some key sources (in order of precedence):

1. **Command-line arguments**
2. **Environment variables**
3. **`application.properties` or `application.yml`**
4. **Default values in code**

> Higher levels override lower ones.

---

## ✅ How to Use Environment Variables in Spring Boot

#### 1. Define Env Variables

 In Linux/macOS:
```bash
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/proddb
export SPRING_DATASOURCE_USERNAME=root
export SPRING_DATASOURCE_PASSWORD=secret
```

In Windows (CMD):
```
set SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/proddb
set SPRING_DATASOURCE_USERNAME=root
set SPRING_DATASOURCE_PASSWORD=secret
```


#### 2. Spring Boot Mapping

Spring Boot automatically maps env variable format to property format.

| Environment Variable     | Becomes Property         |
| ------------------------ | ------------------------ |
| `SPRING_DATASOURCE_URL`  | `spring.datasource.url`  |
| `SERVER_PORT`            | `server.port`            |
| `SPRING_PROFILES_ACTIVE` | `spring.profiles.active` |


#### 3. Using `@Configuration` + `@ConfigurationProperties`

For cleaner management of grouped configs like database or mail settings, use:
###### Step 1: Create a POJO to bind config values

```java
@Component
@ConfigurationProperties(prefix = "spring.datasource")
public class DataSourceConfig {

    private String url;
    private String username;
    private String password;

    // Getters & Setters
}
```

- `@ConfigurationProperties`: Binds all properties that start with the given prefix.

- prefix = `spring.datasource`: Looks for keys like `spring.datasource.url`, `spring.datasource.username`, etc. in  the application.properties.

###### Step 2 (Optional but cleaner): Mark as @Configuration class

If you're grouping multiple configuration classes or manually defining beans inside:
```java
@Configuration
public class AppConfig {
    // You can define custom @Bean methods here if needed
}
```

> `@Configuration` marks the class as a Spring configuration class (like a replacement for XML configs).
> `@Component` + `@ConfigurationProperties` makes it eligible for scanning and binding from environment/properties/yaml.


#### 4. Using with @Value or application.properties

>  Use @Value for quick single values.
> ✅ Use @ConfigurationProperties for structured or grouped config values.

You can reference environment variables like this:

Using `@Value`:
```java
@Value("${spring.datasource.url}")
private String dbUrl;
```

Or fallback with a default:
```java
@Value("${custom.api.key:default-key}")
private String apiKey;
```

Even in application.properties:
```properties
my.secret.key=${MY_SECRET_KEY}
```


---

### 💡 Real-World Example (Docker)

In docker-compose.yml:
```yaml
services:
  myapp:
    image: my-spring-app
    ports:
      - "8080:8080"
    environment:
      - SPRING_DATASOURCE_URL=jdbc:mysql://db:3306/myapp
      - SPRING_DATASOURCE_USERNAME=root
      - SPRING_DATASOURCE_PASSWORD=supersecret
```

Spring Boot will automatically pick up those env variables — no need to hardcode in application.properties.

---
### 🌐 Cloud Example (Heroku, AWS, etc.)

Cloud providers let you define environment variables through UI, CLI, or IaC.

Spring Boot apps will pick them up as long as they're named correctly.

| Approach                 | Use When...                            |
| ------------------------ | -------------------------------------- |
| `application.properties` | Local development, basic setups        |
| Environment Variables    | Secrets, multi-env deploys, production |
| Command-line overrides   | Temporary/test overrides               |
