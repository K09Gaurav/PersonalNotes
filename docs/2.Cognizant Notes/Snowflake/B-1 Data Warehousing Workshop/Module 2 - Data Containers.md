---
tags:
  - accenture
  - snowflake
  - cognizant
---

> [!info]
> **Module Objective**
> Learn how Snowflake organizes data using **Databases → Schemas → Tables**, create and manage these containers, understand worksheet context, and explore metadata using `SHOW` commands.

---

# Quick Revision

| Concept                    | Remember                                                   |
| -------------------------- | ---------------------------------------------------------- |
| Folder                     | Database                                                   |
| Workbook                   | Schema                                                     |
| Worksheet                  | Table                                                      |
| Database                   | Top-level container                                        |
| Schema                     | Groups related tables and other objects                    |
| Table                      | Stores actual data                                         |
| Workspace                  | Modern Snowflake development environment                   |
| Worksheet Context          | Database, Schema, Warehouse, Role                          |
| SHOW DATABASES             | Lists databases                                            |
| SHOW SCHEMAS               | Lists schemas in current database                          |
| SHOW SCHEMAS IN ACCOUNT    | Lists schemas across all accessible databases              |
| First Troubleshooting Step | Verify current context (Role, Database, Schema, Warehouse) |

---

# 1. Project Background

## Scenario

The module introduces **Uncle Yer**, who owns a plant shop and vegetable stand.

Initially, he maintained all records on paper.

As the amount of data increased, Tsai helped him move everything into spreadsheets.

Eventually, spreadsheets became difficult to manage because:

- Data was spread across multiple files.
- Combining data across workbooks became complicated.
- More advanced analysis was difficult.

Instead of continuing to expand spreadsheets, Tsai recommends migrating the data into **Snowflake**.

---

## Why Snowflake?

Tsai recommends Snowflake because:

- Database concepts can better organize growing data.
- Snowflake does **not require expensive upfront licensing**.
- Snowflake offers a **pay-as-you-go pricing model** (with free trial credits).
- It provides an intuitive interface suitable for beginners.

---

## Existing Spreadsheet Structure

Uncle Yer's files were organized like this:

```
House Plants
│
└── Workbooks
    └── Worksheets

Garden Plants
├── Vegetables Workbook
├── Fruits Workbook
└── Flowers Workbook
```

Example:

```
Garden Plants
└── Vegetables Workbook
    ├── Plant Height
    ├── Root Depth
    ├── Soil Needs
    └── ...
```

---

## Spreadsheet Hierarchy vs Snowflake Hierarchy

| Spreadsheet | Snowflake |
|-------------|-----------|
| Folder | Database |
| Workbook | Schema |
| Worksheet | Table |

Migration plan:

```
Garden Plants (Folder)
        │
        ▼
GARDEN_PLANTS (Database)

Vegetables Workbook
        │
        ▼
VEGGIES (Schema)

Plant Height Sheet
        │
        ▼
PLANT_HEIGHT (Table)
```

---

## Core Idea

Snowflake organizes data using hierarchical containers.

```
Database
    │
    ├── Schema
    │      │
    │      ├── Table
    │      ├── View
    │      └── Other Objects
```

This hierarchy makes large datasets easier to organize, query, and maintain than spreadsheets.

---

# 2. Creating Databases and Schemas

## Objective

Create a new database for Uncle Yer's data.

---

## Steps Performed

1. Switch active role to **SYSADMIN**.
2. Create database:

```sql
CREATE DATABASE GARDEN_PLANTS;
```

3. Remove the automatically created PUBLIC schema.

```sql
DROP SCHEMA PUBLIC;
```
![Pasted image 20260704131402](../Images/Pasted%20image%2020260704131402.png)

4. Create three schemas:

```sql
CREATE SCHEMA VEGGIES;

CREATE SCHEMA FRUITS;

CREATE SCHEMA FLOWERS;
```


---

## Resulting Structure

```
GARDEN_PLANTS
│
├── VEGGIES
├── FRUITS
└── FLOWERS
```

Each schema will later contain tables related to its category.
![Pasted image 20260704131446](../Images/Pasted%20image%2020260704131446.png)

---

## Why Remove PUBLIC?

Snowflake automatically creates a **PUBLIC** schema.

Since Uncle Yer already has logical categories:

- VEGGIES
- FRUITS
- FLOWERS

the default PUBLIC schema is unnecessary and can be removed.

> [!note]
> In Snowflake, **DROP** means deleting an object.

---

# 3. Workspaces and SQL Files

## Snowflake Workspaces

Starting September 2025, Snowflake introduced **Workspaces**.

Workspaces combine multiple development tools into one interface.

They replace the older standalone Worksheets.

---

## Workspaces Include

- SQL Editor
- Python Editor
- Notebooks
- Database Explorer
- Query History
- File Manager
- Results Panel

---

## SQL vs Python Files

Snowflake supports:

- SQL files
- Python files

For this course, use **SQL files**.

---

# 4. Worksheet Context

Every SQL worksheet has several context selectors.

These determine where your SQL commands execute.

![Pasted image 20260704131805](../Images/Pasted%20image%2020260704131805.png)


---

## Worksheet Context Settings

Three important context settings are:

- Database
- Schema
- Warehouse

Role is also commonly selected in the worksheet interface because permissions depend on it.

---

## Why Context Matters

Your SQL executes relative to the selected context.

Example:

Current Context

```
Database : GARDEN_PLANTS
Schema   : VEGGIES
Warehouse: COMPUTE_WH
Role      : SYSADMIN
```

Running

```sql
SHOW TABLES;
```

shows tables inside:

```
GARDEN_PLANTS.VEGGIES
```

Changing the schema changes the results without modifying the SQL.

---

## Troubleshooting Tip

> [!tip]
> If you receive a **"Does Not Exist"** error, first verify:
>
> - Current Role
> - Current Database
> - Current Schema
> - Current Warehouse

Incorrect worksheet context is one of the most common causes of SQL errors.

---

# 5. Running SQL Code

A worksheet allows you to:

- Write SQL
- Execute SQL
- View results
- Review execution history

Only the selected statement (or selected text) is executed.

If nothing is selected, Snowflake determines which statement to execute based on the cursor position.


![1345](../Images/Pasted%20image%2020260704131541.png)
![Pasted image 20260704131602](../Images/Pasted%20image%2020260704131602.png)
![Pasted image 20260704131621](../Images/Pasted%20image%2020260704131621.png)


---

# 6. Object Pickers

Object Pickers provide a graphical way to browse Snowflake objects.

They help locate:

- Databases
- Schemas
- Tables
- Views
- Warehouses
- Other objects
![Pasted image 20260704131925](../Images/Pasted%20image%2020260704131925.png)

Instead of typing object names manually, you can browse through the hierarchy.

---

# 7. SHOW Commands

SHOW commands display metadata about Snowflake objects.

Unlike `SELECT`, they do **not** query table data.

Instead, they return information about Snowflake objects.

---

## SHOW DATABASES

Displays all databases visible to the current role.

```sql
SHOW DATABASES;
```
![Pasted image 20260704131943](../Images/Pasted%20image%2020260704131943.png)
Useful for:

- Viewing available databases
- Checking ownership
- Viewing creation dates
- Inspecting metadata

Conceptually similar to opening the first level of an Object Picker.

---

## SHOW SCHEMAS

Displays schemas in the current database context.

```sql
SHOW SCHEMAS;
```

Result depends on the selected database.

Example:
![Pasted image 20260704131952](../Images/Pasted%20image%2020260704131952.png)
![Pasted image 20260704132009](../Images/Pasted%20image%2020260704132009.png)
Current Database

```
GARDEN_PLANTS
```

Result

```
VEGGIES
FRUITS
FLOWERS
```

Changing the current database changes the output.

---

## SHOW SCHEMAS IN ACCOUNT

```sql
SHOW SCHEMAS IN ACCOUNT;
```

Unlike `SHOW SCHEMAS`, this command ignores the current database context.

Instead, it displays **all schemas in all databases** that are visible to the current role.

---

## Context Comparison

| Command | Result |
|----------|--------|
| `SHOW DATABASES` | Lists visible databases |
| `SHOW SCHEMAS` | Lists schemas in the current database |
| `SHOW SCHEMAS IN ACCOUNT` | Lists schemas across all accessible databases |

---

## Context Dependency

```
SHOW SCHEMAS
        │
Uses Current Database
```

```
SHOW SCHEMAS IN ACCOUNT
        │
Ignores Current Database
        │
Searches Entire Account
```

---

# Key Takeaways

- Snowflake organizes data hierarchically:
  - Database → Schema → Table
- Spreadsheet folders map naturally to databases.
- Workbooks map to schemas.
- Worksheets map to tables.
- Snowflake Workspaces replace traditional Worksheets.
- SQL execution depends on worksheet context.
- Context includes Database, Schema, Warehouse, and active Role.
- `SHOW DATABASES` lists databases.
- `SHOW SCHEMAS` lists schemas in the current database.
- `SHOW SCHEMAS IN ACCOUNT` lists schemas across all accessible databases.
- Many SQL errors are caused by incorrect worksheet context rather than missing objects.
