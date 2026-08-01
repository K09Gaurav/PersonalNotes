---
tags:
  - java
  - hibernate
---

### **HibernateUtil.java – What is it and Why Use it?**

`HibernateUtil.java` is a **utility class** that provides a **single, centralized way** to create and manage a `SessionFactory` in Hibernate. Instead of creating a new `SessionFactory` each time manually, this class ensures that a single instance (Singleton Pattern) is used throughout the application.

### **Why Use `HibernateUtil.java`?**

1. **Singleton Pattern** – Ensures only **one** `SessionFactory` instance is created, reducing resource usage.
2. **Encapsulation** – Hides complex Hibernate setup logic.
3. **Code Reusability** – Avoids redundant `SessionFactory` creation in multiple places.
4. **Thread-Safe** – Ensures safe multi-threaded access to `SessionFactory`.
5. **Simplifies Session Management** – Provides a clean and reusable way to get Hibernate `Session` instances.


### **Basic Implementation of** `HibernateUtil.java`
```java
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class HibernateUtil {
    private static SessionFactory sessionFactory;

    static {
        try {
            // Load hibernate.cfg.xml and build SessionFactory
            Configuration configuration = new Configuration();  
			configuration.configure("hibernate.cfg.xml");  
			configuration.addAnnotatedClass(App.class);  
  
			ServiceRegistry serviceRegistry = new StandardServiceRegistryBuilder()  
			        .applySettings(configuration.getProperties())  
			        .build();  
  
			sessionFactory = configuration.buildSessionFactory(serviceRegistry);
        } catch (Exception ex) {
            System.err.println("SessionFactory creation failed: " + ex);
            throw new ExceptionInInitializerError(ex);
        }
    }

    // Method to get SessionFactory
    public static SessionFactory getSessionFactory() {
        return sessionFactory;
    }

    // Method to close SessionFactory (useful when shutting down the app)
    public static void shutdown() {
        if (sessionFactory != null) {
            sessionFactory.close();
        }
    }
}

```

### **Explanation**

**1️⃣ Why is `SessionFactory` Static? Why Not Use an Object?**
  Reason for `static` in `SessionFactory`**
- The `SessionFactory` in Hibernate is designed to be **created only once and shared** throughout the application.
- Making it `static` ensures that **only one instance** exists, preventing unnecessary resource consumption.
- This follows the **Singleton Design Pattern**, which ensures that multiple objects don’t create multiple `SessionFactory` instances.

**2️⃣Check if `SessionFactory` is Already Created :
`if (sessionFactory == null)`
- Ensures that `SessionFactory` is created **only once** (Singleton Pattern).
- If `sessionFactory` is already initialized, the method returns the existing instance instead of creating a new one.

**3️⃣Step 1: Create a Hibernate Configuration Object
`Configuration configuration = new Configuration();`
- **Creates a new Hibernate `Configuration` instance**.
- This object is used to load Hibernate settings (e.g., database URL, username, password).

**4️⃣ Step 2: Load `hibernate.cfg.xml` Configuration File
`configuration.configure("hibernate.cfg.xml");`
- This **loads the Hibernate configuration file** (`hibernate.cfg.xml`) from the classpath.
- Ensures Hibernate gets database connection details, dialect, and entity mappings.
> ✅ **Important:** `hibernate.cfg.xml` should be placed in `src/main/resources/`.

**5️⃣Step 3: Add Annotated Entity Class
`configuration.addAnnotatedClass(App.class);`
- Registers the **entity class (`App.class`)** with Hibernate.
- This is needed **if using annotations (`@Entity`)** instead of specifying mappings in `hibernate.cfg.xml`.
- Ensures Hibernate recognizes the entity for table creation and operations.
> ✅ **Important:** Replace `App.class` with your actual entity class name (e.g., `User.class`, `Employee.class`).

**6️⃣Step 4: Create a `ServiceRegistry` (Required for Hibernate 5+)
```java
ServiceRegistry serviceRegistry = new StandardServiceRegistryBuilder()
        .applySettings(configuration.getProperties())
        .build();
```
- **What is `ServiceRegistry`?**
    - It is an interface introduced in **Hibernate 4+** that acts as a **central registry** for Hibernate services.
    - Required to properly initialize the `SessionFactory` from the configuration settings.
- **How it works?**
    - `applySettings(configuration.getProperties())` → **Reads Hibernate properties** (from `hibernate.cfg.xml`).
    - `build()` → **Builds the registry** with those settings.

**7️⃣Step 5: Build the `SessionFactory`
`sessionFactory = configuration.buildSessionFactory(serviceRegistry);`
- Uses the **Hibernate configuration and service registry** to create the `SessionFactory`.
- This is the **core** of Hibernate, used to open database sessions (`Session` objects).
> ✅ **Important:** Before Hibernate 4, `buildSessionFactory()` was called directly on `Configuration()`. Since Hibernate 4+, using `ServiceRegistry` is the **recommended** approach.