---
tags:
  - java
  - spring
---


Spring Boot supports multiple ways to initialize the database (create tables, insert initial data) when the application starts. Here's how it works:


## 🔸 1. Using schema.sql and data.sql

If placed in src/main/resources, these scripts will run automatically at startup:

| File         | Purpose                                |
| ------------ | -------------------------------------- |
| `schema.sql` | Contains DDL – table creation commands |
| `data.sql`   | Contains DML – insert default records  |

Example – schema.sql:
```sql
DROP TABLE IF EXISTS "widgets";

DROP SEQUENCE IF EXISTS widgets_id_seq;
CREATE SEQUENCE widgets_id_seq INCREMENT 1 MINVALUE 1 MAXVALUE 9223372036854775807 CACHE 1;

CREATE TABLE "widgets" (
    "id" bigint DEFAULT nextval('widgets_id_seq') NOT NULL,
    "name" text,
    "purpose" text,
    CONSTRAINT "widgets_pkey" PRIMARY KEY ("id")
);
```

Example – data.sql:
```sql
INSERT INTO widgets (id, name, purpose) VALUES
(1, 'Widget A', 'Used for testing purposes.'),
(2, 'Widget B', 'Designed for entertainment.'),
(3, 'Widget C', 'Enhances productivity.'),
(4, 'Widget D', 'Perfect for outdoor activities.'),
(5, 'Widget E', 'Improves overall well-being.');
```


> 🟡 These run in order: schema first, then data.

---

## 🔸 2. Enable/Control Execution

Make sure this config is set (if needed):
```properties
spring.sql.init.mode=always
```

This ensures SQL files are run even if a database already exists.

Other values:

- always: always run init scripts
- embedded: only for in-memory DBs (default)
- never: never run them
---
## 🔸 3. Using import.sql (Hibernate-specific)

If using Hibernate, you can place a import.sql in src/main/resources. Hibernate will run it after schema creation.

🟠 Limitation: works only with spring.jpa.hibernate.ddl-auto=create or update.

---

## 🔸 4. Using JPA Annotations (@Entity)

Spring Boot + JPA + Hibernate can auto-create tables from your Java code.

Make sure ddl-auto is set:
```
spring.jpa.hibernate.ddl-auto=update
```

- **create**: drops and recreates every time
- **create**-drop: same as above + drops when app stops
- **update**: updates schema without losing data
- **none**: disables auto-creation
- **validate**: only checks if schema is valid, no creation

Use this with annotated classes:

```java
@Entity
public class User {
  @Id @GeneratedValue
  private Long id;
  private String username;
  private String email;
}
```

---
## 🔸 5. Using Spring @PostConstruct or CommandLineRunner

If you want full control via Java:

```java
@Component
public class DbSeeder implements CommandLineRunner {
    @Autowired
    private UserRepository repo;

    @Override
    public void run(String... args) {
        repo.save(new User("test", "test@mail.com"));
    }
}
```

---


# 🟢 When to Use What?

| Method                   | When to Use                                         |
| ------------------------ | --------------------------------------------------- |
| `schema.sql`, `data.sql` | Simple prototypes or consistent initial DB state    |
| `@Entity + ddl-auto`     | For evolving schema automatically during dev        |
| `import.sql`             | Legacy Hibernate-based setups                       |
| `CommandLineRunner`      | Need conditional or logic-based data initialization |
| Flyway / Liquibase       | For production-grade schema versioning & migrations |
