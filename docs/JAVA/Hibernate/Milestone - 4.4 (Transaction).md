---
tags:
  - java
  - hibernate
---
#### 🔹 What is a Transaction?

- A unit of work that is either **fully completed or not done at all**.
- Ensures **data integrity** in case of failures.
- Follows **ACID** properties.
	- **Atomicity** – All or none.
	- **Consistency**** – Data must be valid according to rules.
	- **Isolation** – Transactions don’t interfere with each other.
	- **Durability** – Once committed, the data is permanent.
#### 🔹 How Hibernate Handles Transactions

- Hibernate uses the **`Transaction` interface** (from `org.hibernate.Transaction`).
- It manages the scope of the unit of work and helps rollback on failure.

#### 🔹Hands-on Example: Add an entity with transaction

```java
// Assume: You have a HibernateUtil class that returns SessionFactory

try (Session session = HibernateUtil.getSessionFactory().openSession()) {
    // Start the transaction (modern way)
    Transaction transaction = session.beginTransaction();

    // Your Entity operation
    Student student = new Student("Rahul", "rahul@email.com");
    session.persist(student); // modern replacement for save()

    // Commit the transaction
    transaction.commit();
} catch (Exception e) {
    e.printStackTrace(); // Log this in real apps
    // transaction will auto-rollback if not committed and Session is closed
}

```

#### 🔹 Key Methods:

- `beginTransaction()`: starts a transaction.
- `commit()`: commits all operations.
- `rollback()`: undoes all operations if something goes wrong.

---
---

### 🔹 Types of Transactions in Hibernate

1. **JDBC Transactions** – Direct handling via `Transaction` object (what you're using now).
2. **JTA (Java Transaction API)** – Used in Java EE apps, more for distributed systems.
3. **Spring-Managed Transactions** – You use `@Transactional` and let Spring manage it.

### 🔹 Transaction Lifecycle (in manual setup)

1. **Start** – `session.beginTransaction()`
2. **Do Work** – `persist()`, `merge()`, `delete()`, etc.
3. **Commit** – `transaction.commit()`
4. **Rollback** – `transaction.rollback()` if exception occurs

### 🔹 Best Practices

✅ Always use `try-with-resources` for sessions  
✅ Wrap transaction code inside `try-catch`  
✅ Always check for `null` before rollback  
✅ Avoid nested transactions unless using a proper framework (like Spring)