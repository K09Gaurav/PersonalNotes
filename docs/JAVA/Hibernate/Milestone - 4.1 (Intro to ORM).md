#java #hibernate

### What is ORM? 🤔

ORM stands for **Object-Relational Mapping**. It’s a technique that allows you to interact with a database using Java objects instead of writing raw SQL queries. Think of it as a **bridge between Java classes and database tables**.

---

### Hibernate Framework

**Hibernate** is the most popular ORM framework or Tool.

- Java Framework that simplifies the development of ==Java Applications to interact with the database==.

WHY ??
- Normally when we create a application which processes and stores data in database.
- Usually we had to manually write SQL queries to do the CRUD Operations.
- But Hibernate will help us do that part now !
- NO NEED to make DAO class (Data Access Objects classes) !
- Those Persistence Logic will be handled by Hibernate.
---
### **Object-Relational Mapping**

- We use ==Objects== to Store Data in Java Applications. 
- Here we are using ==Relational== Database.
- We are ==mapping== our objects to different fields of our table.

>  Hibernate lets you work with simple Java objects (**POJOs - Plain Old Java Objects**) to store and retrieve data.
>  i.e. It is very Lightweight + it is also open source that is also a plus point.

>   Hibernate is a non invasive framework. meaning it wont force the programmers to extend/implement any class/interface.

> [!NOTE]
> HIBERNATE CAN BE USED TO BUILD ANY KIND OF APPLICATION

----

To understand ORM we have to understand how Traditional method works so how does JDBC works.

### Understanding ORM vs. Traditional JDBC

Before diving into ORM, let’s see how things worked traditionally with JDBC :
#### 🔹 The Traditional Way (JDBC)

1. We have a **database** with tables (RDBMS).
2. Our **Java application** needs to store data in these tables.
3. In Java, we store data using **objects**.
4. We create and initialize objects using **getters & setters**.
5. To save an object in the database:
    - We call the **JDBC API**.
    - JDBC uses a **JDBC Driver** to insert data into the table.
6. The problem? **Everything had to be coded manually**:
    - Writing SQL queries for every operation.
    - Creating **DAO (Data Access Object) classes** to manage database interactions.
    - **A LOT of SQL queries** to handle CRUD operations.

>  NOW THIS IS WHERE HIBERNATE COMES IN

#### 🚀 Enter Hibernate (ORM)

1. We still need to store objects in the database, but now:
    - Instead of calling **JDBC**, we use **Hibernate Framework**.
    - We simply give Hibernate the object, and it takes care of saving it to the table.
2. How does Hibernate know where to store the data?
    - **Automatically maps objects to database columns**—no need to write SQL.
💡 **In short:** Hibernate simplifies database operations by handling SQL queries and object mapping for us!


#### ❓ How Does Hibernate Know Where to Store Data?
- We define **entity classes** with annotations like `@Entity` and `@Table`, telling Hibernate how to map them to database tables.
- Hibernate automatically generates the required SQL and executes it.
- It supports multiple **dialects**, meaning it can work with various databases (MySQL, PostgreSQL, Oracle, etc.) without modifying SQL queries manually.

THUS When we create a class we ==map the class with the particular table==.
Then we can explain (MAP) to Hibernate what field is mapped to what column/Attribute.

--- 

