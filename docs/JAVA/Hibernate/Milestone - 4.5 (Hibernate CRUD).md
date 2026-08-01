#java #hibernate 


### 🔹 What is CRUD?

CRUD = **Create, Read, Update, Delete** – the four basic operations you perform on a database entity.


## 🔹 Summary Table (Modern Usage)

| Operation |   Method    | Hibernate Version | Notes                                        |
|:---------:|:-----------:|:-----------------:|:-------------------------------------------- |
|  Create   | `persist()` |     ✅ Modern     | Use this for inserts                         |
|   Read    |  `find()`   |     ✅ Modern     | Replaces `get()`/`load()`                    |
|  Update   |  `merge()`  |     ✅ Modern     | Use for updating detached or fetched objects |
|  Delete   | `remove()`  |     ✅ Modern     | Preferred way to delete                      |


---

##### 1. CREATE (Insert)

```java
try (Session session = HibernateUtil.getSessionFactory().openSession()) {
    Transaction tx = session.beginTransaction();

    Student student = new Student("Ravi", "ravi@email.com");
    session.persist(student);  // Modern method to insert new entity

    tx.commit();
}
```

✔ `persist()` is the preferred way in modern Hibernate (JPA-style).  
❌ Avoid `save()` as it's Hibernate-specific and old-style.


---
##### 2. READ (Fetch)

✅ Using `session.find()` 
```java
try (Session session = HibernateUtil.getSessionFactory().openSession()) {
    Student student = session.find(Student.class, 1); // Fetch student by ID
    System.out.println(student.getName());
}
```

✔ `find()` is the modern JPA-compliant method  
❌ Avoid `get()` and `load()` unless needed for legacy reasons

----
##### 3. UPDATE
```java
try (Session session = HibernateUtil.getSessionFactory().openSession()) {
    Transaction tx = session.beginTransaction();

    Student student = session.find(Student.class, 1); // Fetch first
    student.setEmail("updated@email.com");            // Modify object
    session.merge(student);                           // Update DB

    tx.commit();
}
```

✔ `merge()` is used to update a **detached** object or modify existing ones  
❌ Avoid `update()` (older, Hibernate-specific)

---
##### 4. DELETE

```java
try (Session session = HibernateUtil.getSessionFactory().openSession()) {
    Transaction tx = session.beginTransaction();

    Student student = session.find(Student.class, 1); // Fetch first
    session.remove(student);                         // Delete

    tx.commit();
}
```
✔ `remove()` is the JPA-compliant way to delete  
❌ Avoid `delete()` unless working with Hibernate API directly

