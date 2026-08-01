#java #hibernate 


## 🔗 Hibernate Mapping Techniques – Notes + Hands-on

### 🧱 What is Mapping in Hibernate?

**Mapping** in Hibernate defines how Java classes and their fields relate to database tables and columns. It enables Hibernate to persist Java objects to relational databases seamlessly.

There are two types of mappings:

- **Basic Mapping** – Maps individual fields to table columns.
- **Relationship Mapping** – Maps associations between multiple entity classes.

---

## 🔹 Basic Field Mapping

Use `@Entity`, `@Id`, `@Column`, and other annotations to map fields.

```java
@Entity
@Table(name = "student")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column(name = "student_name")
    private String name;

    private String email;
}
```

### ✅ Notes:

- `@Entity` marks this class as a Hibernate entity.
- `@Table(name = "student")` maps it to the `student` table.
- `@Id` defines the primary key.
- `@GeneratedValue` handles auto-increment strategy.
- `@Column(name = "student_name")` links the field with the DB column.

---

## 🔹 Relationship Mappings

### 1️⃣ One-to-One Mapping

```java
@Entity
public class Student {

    @Id
    private int id;

    @OneToOne(cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    @JoinColumn(name = "laptop_id")
    private Laptop laptop;
}
```

- `@OneToOne`: Declares one-to-one relationship.
- `@JoinColumn`: Specifies the foreign key column.
- `cascade = CascadeType.ALL`: Automatically persists/updates/deletes associated `Laptop` entity.
- `fetch = FetchType.LAZY`: Laptop data is fetched only when accessed (lazy loading).

---

### 2️⃣ One-to-Many Mapping

```java
@Entity
public class Department {

    @Id
    private int id;

    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Employee> employees;
}
```

- `@OneToMany`: A department can have many employees.
- `mappedBy`: Refers to the property in the `Employee` class.
- `cascade = CascadeType.ALL`: Changes to Department cascade to its Employees.
- `fetch = FetchType.LAZY`: Employees are loaded only when accessed.

---

### 3️⃣ Many-to-One Mapping

```java
@Entity
public class Employee {

    @Id
    private int id;

    @ManyToOne(fetch = FetchType.EAGER)
    @JoinColumn(name = "department_id")
    private Department department;
}
```

- `@ManyToOne`: Many employees belong to one department.
- `@JoinColumn`: Creates the foreign key `department_id`.
- `fetch = FetchType.EAGER`: Department is loaded immediately with Employee.

---

### 4️⃣ Many-to-Many Mapping

```java
@Entity
public class Student {

    @Id
    private int id;

    @ManyToMany(cascade = CascadeType.PERSIST)
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses;
}
```

- `@ManyToMany`: A student can enroll in many courses, and each course can have many students.
- `@JoinTable`: Defines the join table and join columns.
- `cascade = CascadeType.PERSIST`: Saves new courses when saving a student.

---

## 🔍 Extra: Bidirectional Relationships

Bidirectional relationships allow both entities to be aware of each other.

### Example: One-to-Many & Many-to-One

```java
@Entity
public class Department {

    @Id
    private int id;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees;
}

@Entity
public class Employee {

    @Id
    private int id;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}
```

- `mappedBy` on one side tells Hibernate that the relationship is controlled by the other side.

✅ Keeps data consistent in both directions.

---

## 🔁 Cascade Types

- `PERSIST` – Save child entities automatically
- `MERGE` – Update child entities
- `REMOVE` – Delete child entities
- `ALL` – Applies all above operations

---

## 🚦 Fetch Types

- `LAZY` – Loads data only when accessed (better performance)
- `EAGER` – Loads data immediately (may cause performance issues if not managed)

---

✅ All annotations and code patterns used here are up-to-date and follow modern Hibernate standards (Hibernate 5.2+ and above).

📌 The HQL portion you previously wrote also uses current and non-deprecated APIs:

- `createQuery(hql, Class<T>)` is type-safe and recommended.
- `getResultList()` and `setParameter()` are standard.
- `uniqueResult()` is valid in Hibernate 5+, though `getSingleResult()` is preferred in newer versions for strict non-null expectations.

Let me know if you want to update the HQL section to replace `uniqueResult()` with `getSingleResult()` for stricter behavior.