---
tags:
  - java
  - spring
---

>Focus: **Annotations** + **Lightweight Configuration**  
>So you know what Spring Boot is automating for you

---

## 🔹 1. SPRING ANNOTATIONS (THE CORE FOUR)

|Annotation|What It Means|Where You Use It|
|---|---|---|
|`@Component`|Marks a **generic class** to be managed by Spring|Any class you want Spring to create and manage|
|`@Service`|Marks a **service class** (business logic layer)|In your core logic, like `UserService`, `OrderService`|
|`@Repository`|Marks a **DAO class** (data access layer)|Classes that talk to DB: `UserRepository`, etc.|
|`@Controller` / `@RestController`|Marks a **web controller**|For handling browser/API requests (explained more in Boot)|
 ✅ What These Do:

All of them are **variations of `@Component`**. They tell Spring:
> “Please manage this class as a bean in your system.”

📌 When you use any of these, Spring **automatically creates** an object and **injects it wherever needed**.

---

### 🔹 `@Autowired` — Dependency Injection

Use this when you want Spring to **inject a dependency** into a class:

```java
@Component
class Engine {}

@Service
class CarService {
    @Autowired
    private Engine engine;
}
```

🔍 Spring looks at `@Autowired` and says:

> “Oh! `CarService` needs an `Engine`. I already have one. Let me plug it in.”

💡 Works with:
- Fields (not recommended for testing)
- Setters
- Constructors (recommended)

---

## 🔹 2. MINIMAL CONFIGURATION — THE SPRING WAY

### A. Java-Based Configuration with `@Configuration` and `@Bean`

This is how you'd define beans manually **before** Spring Boot.

```java
@Configuration
public class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine();
    }

    @Bean
    public Car car() {
        return new Car(engine());
    }
}
```

🧠 Meaning:

- `@Configuration`: This is a **Spring config file** (in Java)
- `@Bean`: “Hey Spring, I want you to manage this method’s return value as a bean.”

⚠️ Spring Boot doesn't usually require this unless you're doing something custom.

---

### B. Component Scanning with `@ComponentScan`

If you want Spring to **auto-discover your beans**, you tell it:

`@ComponentScan(basePackages = "com.example")`

Spring will search that package for `@Component`, `@Service`, etc., and **register them automatically**.

📌 In Spring Boot, this happens **automatically** in the main class.

---

## ✅ Summary Table: Minimal Required Knowledge

|Concept|Use|Annotation|
|---|---|---|
|Marking a Spring-managed class|So Spring can create & inject it|`@Component`, `@Service`, etc.|
|Injecting dependencies|So you don’t `new` objects manually|`@Autowired`|
|Defining beans manually (rare in Boot)|Custom creation logic|`@Configuration`, `@Bean`|
|Letting Spring find components|So you don't list all manually|`@ComponentScan` (auto in Boot)|
## 🔥 The Truth for Spring Boot

In Spring Boot:

- You don’t write `@ComponentScan` — it’s **automatic**
- You rarely need `@Bean` or `@Configuration` — Boot uses **starters and autoconfig**
- You focus mostly on:
    - `@Service`, `@Repository`, `@RestController`
    - `@Autowired`
    - `@SpringBootApplication` (combo of multiple things)
