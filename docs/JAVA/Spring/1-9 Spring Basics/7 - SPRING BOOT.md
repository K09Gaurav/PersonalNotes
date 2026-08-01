#spring #java
# Spring Boot Architecture Overview

Spring Boot is a **layer on top of the Spring Framework**, designed to simplify development by auto-configuring many parts of your application.

---

## Application Layering

A typical Spring Boot application is structured into logical layers:

- **Presentation Layer**: Handles HTTP requests (controllers, REST APIs).
- **Service Layer**: Contains business logic and service classes.
- **Persistence Layer**: Handles database interactions.


---

## Persistence Layer

This layer is responsible for **communicating with the database**.

- It deals with **entities** — Java objects that map to database tables.
- These entities represent the application's **domain model**.

### Data Access Patterns:

To interact with the database, two main patterns are used:

1. **Repository Pattern**  
   - Commonly used with Spring Data JPA.  
   - Leverages interfaces like `JpaRepository` or `CrudRepository`.

2. **DAO (Data Access Object) Pattern**  
   - Explicitly creates DAO classes with database methods using `JdbcTemplate`, `EntityManager`, etc.

> The primary operations in this layer are **CRUD** (Create, Read, Update, Delete),  
> but you can define custom queries and logic based on your application's needs.

**GOAL**  : Handle all interaction with your persistence technology lkike database 

and you would like to expose them via well defined interfafces and because of those interfaces you can change those interfaces you can completely change / replace the persistence technology and the rest of application wouldnt have to worry about it.

---
## Service Layer

**Goal:** To use the functionality provided by the **persistence layer** and fulfill the application's business requirements.

- Typically implemented using **interfaces** and their corresponding **service classes**.
- Can contain:
  - Business logic
  - Validation
  - Data transformation
  - Or just pass-through calls to the persistence layer (in simple cases)

> **Why it matters:**  
>It decouples the presentation layer from direct access to the database layer.  
>This makes the application easier to test, maintain, and extend.

---

## Presentation Layer

**Goal:** To expose data (processed by the service layer) to the outside world — typically to the user or client applications.

- Interfaces with the **service layer** to get data and serve it via:
  - **REST APIs** (common with Spring Boot)
  - **GraphQL APIs**
  - **Web Socket endpoints**
  - **MVC Controllers** (for web apps)

> This is where you decide *how* to present your data.  
For example, switching from REST to GraphQL requires changes **only** in the presentation layer — not in service or persistence.

---

# Modularity in Spring vs Spring Boot

Spring Boot builds on top of the **Spring Framework** and simplifies dependency management by **auto-configuring** and **bundling common modules**.

If we had used **Spring (without Spring Boot)**, we would have to manually include and configure several core modules, such as:

| Module              | Purpose |
|---------------------|---------|
| `spring-core`       | Core utilities and the IoC container. |
| `spring-context`    | Application context, bean lifecycle management. |
| `spring-beans`      | Dependency injection and bean configuration. |
| `spring-aop`        | Aspect-Oriented Programming support. |
| `spring-web`        | Basic web stack and servlet handling. |
| `spring-webmvc`     | MVC and REST support (controllers, routing). |
| `spring-jdbc`       | JDBC integration and DataSource configuration. |
| `spring-tx`         | Transaction management. |
| `spring-orm`        | Integration with ORM tools like Hibernate. |
| `spring-test`       | Testing support for Spring components. |

> With **Spring Boot**, most of these are pulled in automatically via `spring-boot-starter` dependencies and are auto-configured out of the box.

## Benefit of Spring Boot

- Less boilerplate
- No manual XML config
- Rapid setup with sensible defaults
- Easy to customize when needed

---
# Inversion of Control (IoC)

In traditional programming, a class often creates its own dependencies like this:

```java
ServiceA serviceA = new ServiceA();
```
This works initially, but causes problems later:

- Tightly couples the class to specific implementations.
- Changing the dependency (e.g., replacing `ServiceA` with `ServiceB`) requires modifying the class code.
- Hard to test or extend.

## Better Way: Inversion of Control

Instead of creating the dependency, we **declare what we need** — usually by referring to an interface:
`private final MyService service;`

Now, something else (like Spring) is responsible for:

- Creating the object.
- Choosing the implementation.
- Injecting it where needed.

This is called **Inversion of Control (IoC)**:

> You give up control of dependency creation and let the framework handle it.

## Benefits

- **Loose coupling**: Easier to replace or extend implementations.
- **Easier testing**: Can inject mock versions.
- **More flexible and maintainable** design.

## Spring's Role

Spring implements IoC using the **Dependency Injection (DI)** pattern:

- You define interfaces.
- Spring creates and injects the concrete classes.
- Changing an implementation is as simple as:
    - Writing a new class that implements the interface.
    - Letting Spring inject the new one automatically.

> No need to change your business logic classes.