
> [!info]
> **Module Objective**
> Learn how Snowflake manages databases, schemas, roles, ownership, and access control using **RBAC (Role-Based Access Control)** and **DAC (Discretionary Access Control)**.

#accenture #snowflake #cognizant 

---

## Quick Revision

| Concept                    | Remember                    |
| -------------------------- | --------------------------- |
| Database                   | Stores schemas              |
| Schema                     | Stores objects              |
| INFORMATION_SCHEMA         | Metadata, cannot be deleted |
| PUBLIC                     | Default editable schema     |
| Role                       | Collection of privileges    |
| RBAC                       | Access through roles        |
| DAC                        | Creator role owns object    |
| Owner                      | Role with full control      |
| Default Role               | Active after login          |
| Warehouse                  | Compute engine              |
| Database                   | Storage layer               |
| First Troubleshooting Step | Check your current role     |


---

## 1. Creating a Database

### Steps

1. Open **Catalog**
2. Click **+ Database**
3. Enter a database name (e.g., `DEMO_DB`)
4. Click **Create**
![Pasted image 20260704124429](../Images/Pasted%20image%2020260704124429.png)
![Pasted image 20260704124441](../Images/Pasted%20image%2020260704124441.png)
> [!note]
> Every newly created database automatically contains two default schemas.

---

## 2. Database Organization

### Database Hierarchy

```
Account
└── Database
    ├── INFORMATION_SCHEMA
    └── PUBLIC
```

A **Database** is used to organize related datasets.

A **Schema** is a logical container inside a database that stores objects like:

- Tables
- Views
- Stages
- File Formats
- Procedures
- Functions
- Sequences
- Tasks
- Streams
- ![Pasted image 20260704124505](../Images/Pasted%20image%2020260704124505.png)

---

### Default Schemas

#### INFORMATION_SCHEMA

Purpose:

- Contains metadata about database objects.
- Stores system-generated views.
- Used for querying metadata.

Characteristics:

- Created automatically.
- Cannot be deleted.
- Cannot be renamed.
- Cannot be moved.

Examples of information stored:

- Tables
- Columns
- Views
- Privileges
- Other metadata

---

#### PUBLIC

Purpose:

- Default working schema.
- Used to store user-created objects.

Characteristics:

- Created automatically.
- Initially empty.
- Can be renamed.
- Can be deleted.
- Can be moved.

Objects commonly stored:

- Tables
- Views
- Procedures
- Functions
- Other database objects

---

### Exam Point

Every new Snowflake database contains exactly **two default schemas**:

- `INFORMATION_SCHEMA`
- `PUBLIC`

---

## 3. Database Ownership

Every database has an **Owner Role**.

The owner role can:

- Rename the database
- Delete the database
- Transfer ownership
- Grant privileges
- Manage database properties

---

### Ownership Transfer

Snowflake allows ownership to be transferred after an object has been created.

Example:

```
ACCOUNTADMIN
	│
Creates DEMO_DB
	│
Transfer Ownership
	▼
SYSADMIN
```

![Pasted image 20260704124539](../Images/Pasted%20image%2020260704124539.png)
![Pasted image 20260704124545](../Images/Pasted%20image%2020260704124545.png)
After transfer:

- SYSADMIN becomes the owner.
- ACCOUNTADMIN still retains effective control because it is a higher role in the hierarchy.


#### Switch Your System Role Back to SYSADMIN

![Pasted image 20260704124724](../Images/Pasted%20image%2020260704124724.png)

---

### Important Facts

- Objects are owned by **roles**, not users.
- Ownership can be transferred.
- Ownership determines who has full control over an object.

---

## 4. Identity vs Access

### Identity

Identity answers:

> **Who are you?**

Examples:

- User account
- Username
- Login credentials
- Authentication

Identity verifies the user.

---

### Access

Access answers:

> **What are you allowed to do?**

Examples:

- Read data
- Create databases
- Drop tables
- Manage users
- Execute queries

Access is controlled using **Roles**.

---

### Identity vs Access

| Identity | Access |
|-----------|---------|
| Who the user is | What the user can do |
| Authentication | Authorization |
| User account | Role & Privileges |

---

## 5. Roles in Snowflake

### What is a Role?

A **Role** is a collection of permissions.

Instead of assigning permissions directly to users, Snowflake assigns permissions to **roles**, and roles are assigned to users.

This is the basis of **Role-Based Access Control (RBAC).**

---

### Changing Active Role

A user may have multiple roles.

Only **one role is active at a time**.

Changing the active role changes:

- Visible databases
- Visible schemas
- Available warehouses
- Allowed operations

If an object suddenly disappears, the first thing to check is:

> **Current Role**

---

## 6. Snowflake System Roles

### Role Hierarchy

```
ACCOUNTADMIN
│
├── SECURITYADMIN
│
├── SYSADMIN
│
└── USERADMIN
```

![Pasted image 20260704124821](../Images/Pasted%20image%2020260704124821.png)
The hierarchy allows higher roles to inherit privileges from lower roles.

---

### ACCOUNTADMIN

Highest privileged system role.

Responsibilities:

- Complete account administration
- Manage warehouses
- Manage databases
- Manage security
- Manage billing
- Manage roles

Typically used only for administrative work.

---

### SYSADMIN

Responsible for:

- Databases
- Schemas
- Tables
- Warehouses
- Data objects

Often considered the primary role for creating database objects.

---

### SECURITYADMIN

Responsible for:

- Roles
- Privileges
- Grants
- Security management

---

### USERADMIN

Responsible for:

- Creating users
- Managing users

---

### Role Inheritance

Snowflake roles inherit permissions.

Think of the hierarchy like a family tree.

```
ACCOUNTADMIN
       │
       ├──── SYSADMIN
       │
       ├──── SECURITYADMIN
       │
       └──── USERADMIN
```

Higher roles inherit permissions from lower roles.

---

## 7. RBAC (Role-Based Access Control)

### Definition

RBAC controls access using **Roles** instead of assigning permissions directly to users.

Flow:

```
User
   │
Assigned Role
   │
Role contains Privileges
   │
Privileges allow Access
```

---

### Advantages

- Easier administration
- Better security
- Reusable permission sets
- Scalable access management

---

### Troubleshooting Rule

If Snowflake reports:

- Object does not exist
- Database not found
- Schema not found

First check:

> **Current Role**

Many "does not exist" errors are actually permission issues.

---

## 8. DAC (Discretionary Access Control)

### Definition

DAC follows the rule:

> **You create it, you own it.**

The role that creates an object automatically becomes its owner.

---

Example

```
Current Role = SYSADMIN

Create Database
        │
        ▼
SYSADMIN becomes Owner
```

If the active role changes:

```
Current Role = ACCOUNTADMIN

Create Database
        │
        ▼
ACCOUNTADMIN owns it
```

Ownership depends on the **active role**, not the user.

---

### Snowflake Uses Both Models

Snowflake combines:

#### RBAC

Controls:

- Privileges
- Permissions
- Access

#### DAC

Controls:

- Ownership

Together they provide secure access management.

---

### Important Rule

Snowflake:

- Assigns **Privileges** to Roles.
- Assigns **Ownership** to Roles.

Not directly to users.

---

## 9. Default Role

Every user has a **Default Role**.

Purpose:

- Automatically selected when the user logs in.

For Trial Accounts:

```
Default Role = ACCOUNTADMIN
```

---

### Important

Changing to another role during a session:

```
ACCOUNTADMIN
      │
Switch
      ▼
SYSADMIN
```

works normally.

After logging out and logging back in:

```
Role
▼
Returns to Default Role
```

---

Default Role only affects:

- Initial login role.

It does **not** prevent switching to other assigned roles.

---

## 10. Ownership vs Access

Ownership automatically provides full access.

However, simply owning a parent object does not always guarantee visibility of child objects if ownership differs.

Example:

```
Database Owner
      │
ACCOUNTADMIN

Schema Owner
      │
ACCOUNTADMIN
```

If the database ownership changes:

```
Database
▼
SYSADMIN

Schema
▼
ACCOUNTADMIN
```

SYSADMIN may not see the schema until ownership (or privileges) is updated.

---

### Challenge Concept

Transfer ownership of the **PUBLIC** schema to **SYSADMIN** so it becomes visible while using the SYSADMIN role.

---

## 11. Creating Objects with the Correct Role

Best Practice:

Before creating an object:

1. Switch to the intended owner role.
2. Create the object.

Example:

```
Switch Role
    │
SYSADMIN
    │
Create UTIL_DB
    │
Owner = SYSADMIN
```

This avoids needing ownership transfers later.

![Pasted image 20260704125300](../Images/Pasted%20image%2020260704125300.png)

---

## 12. Warehouses

### What is a Warehouse?

A Warehouse is Snowflake's **compute engine**.

Responsibilities:

- Execute SQL queries
- Perform computations
- Load data
- Transform data

Unlike traditional databases, warehouses **do not store data**.

![Pasted image 20260704125321](../Images/Pasted%20image%2020260704125321.png)

---

### Data vs Compute

| Component | Purpose |
|------------|----------|
| Database | Stores data |
| Warehouse | Performs computation |

---

### Warehouses in Trial Account

#### COMPUTE_WH

Purpose:

- General compute warehouse
- Used for course labs

Default Owner:

- ACCOUNTADMIN

---

#### SNOWFLAKE_LEARNING_WH

Purpose:

- Default learning warehouse

Owner:

- ACCOUNTADMIN

---

#### SYSTEM$STREAMLIT_NOTEBOOK_WH

Purpose:

- Used internally for Streamlit apps and notebooks.

Not intended for direct user interaction.

---

### Warehouse Ownership

Ownership can also be transferred.

Example:

```
ACCOUNTADMIN
      │
Transfer Ownership
      ▼
SYSADMIN
```

![Pasted image 20260704125403](../Images/Pasted%20image%2020260704125403.png)
This allows SYSADMIN to use and manage the warehouse.

---

## 13. Troubleshooting Missing Objects

If a schema or database appears to be missing:

1. Check current role.
2. Switch to ACCOUNTADMIN if necessary.
3. Refresh the browser.
4. Verify ownership.
5. Transfer ownership if required.
6. Switch back to SYSADMIN.
7. Refresh again.

> [!tip]
> Most "Object does not exist" errors in Snowflake are caused by using the wrong role rather than the object actually being missing.

---

## Key Takeaways

- Every database automatically contains:
  - `INFORMATION_SCHEMA`
  - `PUBLIC`
- Objects are owned by **Roles**, not users.
- The active role at object creation becomes the owner.
- Snowflake combines **RBAC** and **DAC**.
- **RBAC** manages permissions.
- **DAC** manages ownership.
- Roles can inherit permissions through a hierarchy.
- Only one role is active at any time.
- Default role is used only during login.
- Warehouses provide **compute**, while databases provide **storage**.
- Before assuming an object is missing, always check the **current role**.

