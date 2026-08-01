#java #hibernate


### What is Hibernate? 🔥

**Hibernate** is the most popular ORM framework in Java. It takes care of mapping your Java objects to database records, so you don’t have to write a ton of SQL. Instead of manually handling `ResultSet`, `PreparedStatement`, and JDBC code, Hibernate lets you work with simple Java objects (**POJOs - Plain Old Java Objects**) to store and retrieve data.

---
##### Imagine You Have a Notebook 📒

Think of a **Java object** like a page in a notebook where you write down some information.  
Think of a **database** like a big bookshelf where you store all your notebooks.

Normally, if you want to **save** or **read** information from the bookshelf (database), you’d have to write special instructions (**SQL queries**) like:  
👉 _“Write ‘John Doe’ in the notebook on shelf 3, row 5.”_  
👉 _“Find the notebook where the name is ‘John Doe’ and tell me what’s written inside.”_

**Hibernate** is like a smart librarian 🧑‍🏫 who does this for you automatically!  
Instead of writing complicated instructions, you just say:  
👉 _“Hey Hibernate, save this User object!”_  
👉 _“Hey Hibernate, find me a user named John Doe!”_

And Hibernate figures out how to do that in the database. ✅

---
### Why Use Hibernate?

Here’s why Hibernate is a big deal:
1. **No more SQL headaches** – You write Java code instead of SQL.
2. **Automatic Table Mapping** – Hibernate figures out how to save Java objects as rows in a database.
3. **Faster Development** – No need to write repetitive database code.
4. **Database Independence** – Works with multiple databases (MySQL, PostgreSQL, Oracle, etc.) without changing your code.
5. **Built-in Caching** – Improves performance by storing frequently used data.

### How Hibernate Works (Simplified)

1. **You create a Java class** (e.g., `User`)
    
2. **You map it to a database table** (using annotations or XML)
    
3. **Hibernate handles saving, retrieving, and updating records automatically!**

Example :
```java
@Entity  // Marks this class as a database entity
@Table(name = "users")  // Maps to a table named 'users'
public class User {
    
    @Id  // Marks this as the primary key
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Auto-increment ID
    private Long id;

    private String name;
    private String email;

    // Getters and Setters
}
```

Saving a user in Database with Hibernate:

```java
SessionFactory sessionFactory = new Configuration().configure("hibernate.cfg.xml").buildSessionFactory();
Session session = sessionFactory.openSession();

Transaction transaction = session.beginTransaction();
User user = new User();
user.setName("John Doe");
user.setEmail("john.doe@example.com");

session.save(user);  // Hibernate converts this to an INSERT SQL query
transaction.commit();
session.close();
```


---
----
### Me doing it !!

#### Setting Up Hibernate with MySQL in a Maven Project

1. **Created a Maven Project** – _Why use Maven?_
    - Maven simplifies dependency management, so we don’t have to manually download and configure JAR files.
    - It provides a structured project format, making it easier to manage and build applications.
    - It automates compilation, testing, and packaging, improving project efficiency.
        
2. **Configured `pom.xml`**
    - Added the necessary dependencies:
        - Hibernate (for ORM functionality)
        - MySQL Connector (to interact with the database)

3. **Database Configuration**
    - Hibernate needs to know details about our database, including:
        - Database Name
        - Connection URL
        - Username & Password
        - Driver Class
            
4. **Using an XML File for Configuration**
    - We will store these database details in an XML file.
    - The file follows a **DTD (Document Type Definition)** to define its structure:
```java
<!DOCTYPE hibernate-configuration PUBLIC  
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"  
        "https://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
```

5. **Adding Hibernate Configurations**
	- Hibernate uses a **`SessionFactory`** to manage database sessions.
	- All configurations are defined inside the `<session-factory>` tag.
	- Essential properties include:
	    1. **Database Driver** – Specifies which JDBC driver to use.
	    2. **Database URL** – Connection string to the database.
	    3. **Username & Password** – Credentials for database access.
	    4. **Dialect** – Tells Hibernate how to generate SQL for the specific database type.
	    5. **Additional Properties**:
	        - `hbm2ddl.auto=update` – Automatically creates/updates tables based on entity classes.
	        - `show_sql=true` – Logs the SQL queries Hibernate executes.

**Configuration file (`hibernate.cfg.xml`):**
```xml
<hibernate-configuration>
    <session-factory>
        <!-- Database Connection Settings -->
        <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="connection.url">jdbc:mysql://localhost:3306/MyHiber</property>
        <property name="connection.username">root</property>
        <property name="connection.password">root</property>

        <!-- Hibernate SQL Dialect -->
        <property name="dialect">org.hibernate.dialect.MySQLDialect</property>

        <!-- Hibernate Properties -->
        <property name="hbm2ddl.auto">update</property>
        <property name="show_sql">true</property>
    </session-factory>
</hibernate-configuration>
```

>  A little on Dialects and Additional Hibernate Properties:
>  -  Hibernate Dialects:
> 	A **dialect** in Hibernate tells the framework how to generate SQL queries specific to the database you are using. Different databases have different SQL syntax and behaviors, and Hibernate needs to adjust accordingly.
> 	For example, MySQL uses backticks ( \` ) for table and column names, whereas PostgreSQL uses double quotes ("). Hibernate’ s dialect handles these differences automatically.
> 	Some common dialects:
> 	- **MySQL:** `org.hibernate.dialect.MySQLDialect`
> 	- **PostgreSQL:** `org.hibernate.dialect.PostgreSQLDialect`
> 	- **Oracle:** `org.hibernate.dialect.OracleDialect`
> 	- **SQL Server:** `org.hibernate.dialect.SQLServerDialect`
>  - Additional Hibernate Properties
> 	These properties help configure Hibernate’ s behavior when interacting with the database.
> 	
> 	 1. `hbm2ddl.auto` (Database Schema Management)
> 		Full form -> Hibernate Mapping to Data Definition Language (DDL).
> 		This property controls how Hibernate handles table creation and updates based on Java entity classes.
> 		Options:
> 		- `create` → Drops existing tables (if any) and creates new ones every time the application starts.
> 		- `update` → Modifies the database schema if needed but keeps existing data.
> 		- `create-drop` → Like `create`, but also drops the tables when the session factory closes.
> 		- `validate` → Only checks if the schema matches the entity classes but does not modify the database.
> 		- `none` → No automatic schema creation or validation.
> 
> 	1.  `show_sql` (SQL Logging)
> 		This property enables logging of SQL statements executed by Hibernate.
> 		When set to `true`, it prints SQL queries to the console, helping with debugging and performance analysis.


#### Integrating Hibernate in Maven Project
1. Creating Session Factory: `SessionFactory factory = new Configuration().configure().buildSessionFactory();`
	- This initializes Hibernate and creates a session factory.
2. **Before using this**, ensure that `hibernate.cfg.xml` is in the correct location.
	- Location should be : `src/main/resources/hibernate.cfg.xml`
3. Alternative: Manually Loading `hibernate.cfg.xml`
	- If you don’t want to rely on the default class-path, manually specify the file path:
```java
String hibernatePropsFilePath = "src/main/resources/hibernate.cfg.xml";  
File hibernatePropsFile = new File(hibernatePropsFilePath);  
Configuration configuration = new Configuration();  
configuration.configure(hibernatePropsFile);
```
- This method **reads from the file system** instead of the class path.
- Works even if `src/main/resources` is missing, but not recommended for production.
- Not rerecommended because class path-based loading (`configure()`) is preferable because it's **portable** and works across different environments without hardcoded file paths.

>✅ **Issue:** `hibernate.cfg.xml` not found.  
>✔ **Fix:** Ensure `src/main/resources` exists and contains `hibernate.cfg.xml`.
>
> ✅ **Issue:** Minimal Hibernate logs appear (only version info).  
> ✔ **Fix:** Make sure Hibernate loads the config from the classpath instead of manually using `File`.
> 
> ✅ **Issue:** if you cant import `org.hibernate` package
> 	Step 1: in Maven Dependencies folder check if "hibernate-core" jar is present or not 
> 	Step 2: if not present then open pom.xml, in hibernate-core dependency remove this line -->` <type>pom</type> `
> 	Step 3: update maven project 
> 	Step 4: Now in Maven Dependencies folder you will find "hibernate-core" jar. 
> 	Step 5: now you can import `org.hibernate` package
