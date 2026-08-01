---
tags:
  - java
  - hibernate
---

## 📌 Hibernate Query Language (HQL)

---
## 🔍 What is HQL?

**Hibernate Query Language (HQL)** is an object-oriented query language provided by Hibernate. It allows you to query and manipulate data using **Java class and field names**, rather than table and column names as in SQL.

✅ Works with **entities and their properties**  
❌ Does **not** use raw table or column names

---

## 🔁 SQL vs HQL – Quick Comparison

|SQL|HQL|
|---|---|
|`SELECT * FROM student`|`FROM Student`|
|`SELECT name FROM student`|`SELECT s.name FROM Student s`|
|`WHERE email = 'abc@x.com'`|`WHERE s.email = 'abc@x.com'`|

---

## 🧾 Basic HQL Syntax

```java
String hql = "FROM Student"; // Fetch all students
List<Student> students = session.createQuery(hql, Student.class).getResultList();
```

✔ Uses the entity class name (`Student`)  
✔ Refers to **Java field names** like `name`, `email`  
✔ `createQuery()` with class type provides **type-safety** (Hibernate 5.2+)

###### ✅ `session.createQuery(hql, Student.class)`

- **Purpose**: Creates a type-safe query using HQL.
- `hql`: This is a string that contains your HQL query, like `"FROM Student"`.
- `Student.class`: Tells Hibernate what type of result you're expecting (i.e., list of `Student` objects).

###### ✅ `getResultList()`

- **Purpose**: Executes the query and returns a `List` of results.
- **Use When**: You expect **multiple results**.
- **Returns**: `List<Student>` or `List<Object[]>` depending on the query.

---

## 🔨 Common HQL Queries

### 1️⃣ SELECT All Records

```java
String hql = "FROM Student";
List<Student> list = session.createQuery(hql, Student.class).getResultList();
```

---
### 2️⃣ SELECT with WHERE Clause

```java
String hql = "FROM Student s WHERE s.name = :name";
Student result = session.createQuery(hql, Student.class)
                        .setParameter("name", "Ravi")
                        .uniqueResult();
```
###### ✅ `setParameter("param", value)`

- **Purpose**: Sets the value for a named parameter (`:param`) in your HQL query.
- **Use Case**: Prevents SQL injection, cleaner syntax.
###### ✅ `uniqueResult()`

- **Purpose**: Returns **a single object** (or `null`) if the query matches **only one row**.
- **Use When**: Your query is expected to return just one result.
---
### 3️⃣ SELECT Specific Fields (Returning Object[])

```java
String hql = "SELECT s.name, s.email FROM Student s";
List<Object[]> result = session.createQuery(hql).getResultList();
for (Object[] row : result) {
    System.out.println("Name: " + row[0] + ", Email: " + row[1]);
}
```

The result is not a list of `Student` objects but a `List<Object[]>`, where each `Object[]` holds selected fields

---

### 4️⃣ UPDATE Using HQL

```java
String hql = "UPDATE Student SET email = :email WHERE id = :id";
Transaction tx = session.beginTransaction();
int rows = session.createQuery(hql)
                  .setParameter("email", "new@email.com")
                  .setParameter("id", 1)
                  .executeUpdate();
tx.commit();
```

###### ✅ `executeUpdate()`

- **Purpose**: Executes an **UPDATE** or **DELETE** query.
- **Returns**: Number of rows affected.
- **Requires**: A transaction to be active.
---
### 5️⃣ DELETE Using HQL

```java
String hql = "DELETE FROM Student WHERE id = :id";
Transaction tx = session.beginTransaction();
session.createQuery(hql)
       .setParameter("id", 1)
       .executeUpdate();
tx.commit();
```

---

## 📎 Key Takeaways

- Always use **entity class names** and **Java field names** in HQL.
- Use `createQuery(hql, Class)` for **type safety and cleaner syntax**.
- Always wrap **UPDATE** and **DELETE** operations in a transaction.
- You can use **named parameters** (`:paramName`) or **indexed parameters** (`?1`) in queries.
---

## Questions Practice

## 🧪 Mini Hands-On Examples

### 1️⃣ Get all students who scored more than 75 marks

```java
String hql = "FROM Student s WHERE s.marks > :minMarks";
List<Student> students = session.createQuery(hql, Student.class)
                                .setParameter("minMarks", 75)
                                .getResultList();
```

### 2️⃣ Update the email of a student whose ID is 5

```java
String hql = "UPDATE Student SET email = :email WHERE id = :id";
Transaction tx = session.beginTransaction();
int updatedRows = session.createQuery(hql)
                         .setParameter("email", "updated@example.com")
                         .setParameter("id", 5)
                         .executeUpdate();
tx.commit();
```

### 3️⃣ Delete all students with marks less than 30

```java
String hql = "DELETE FROM Student WHERE marks < :cutoff";
Transaction tx = session.beginTransaction();
int deletedRows = session.createQuery(hql)
                         .setParameter("cutoff", 30)
                         .executeUpdate();
tx.commit();
```

### 4️⃣ Select only `name` and `marks` of all students and print them

```java
String hql = "SELECT s.name, s.marks FROM Student s";
List<Object[]> result = session.createQuery(hql).getResultList();
for (Object[] row : result) {
    System.out.println("Name: " + row[0] + ", Marks: " + row[1]);
}
```

---

## 🔁 Recap: Flow of HQL Queries

1. Open a Hibernate `Session`.
2. Create an HQL query string.
3. Use `createQuery()` and provide result type (if applicable).
4. Bind any parameters using `setParameter()`.
5. For reads → use `getResultList()` or `uniqueResult()`  and For updates/deletes → use `executeUpdate()` with a `Transaction`.