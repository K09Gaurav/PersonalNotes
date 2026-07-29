---
tags:
  - accenture
  - snowflake
  - cognizant
---

> [!info]
> **Module Objective**
> Learn how Snowflake Worksheets work, understand worksheet context settings, explore the purpose of Virtual Warehouses, and understand warehouse sizing, scaling, and cost management.

 
---
# Quick Revision

| Concept | Remember |
|----------|----------|
| Worksheet | SQL editor for writing and running queries |
| Worksheet Context | Database, Schema, Role, Warehouse |
| Required Context | Role, Warehouse |
| Convenience Context | Database, Schema |
| Fully Qualified Name | `DATABASE.SCHEMA.OBJECT` |
| First Troubleshooting Step | Check Current Role |
| Warehouse | Compute engine (not storage) |
| Cluster | Group of servers |
| Server | Performs computation |
| Scale Up | Increase warehouse size (more servers) |
| Scale Down | Decrease warehouse size (fewer servers) |
| Scale Out | Add clusters |
| Scale In | Remove extra clusters (**Snap Back**) |
| Auto Suspend | Stops idle warehouse automatically |
| Auto Resume | Restarts warehouse when needed |
| Resource Monitor | Tracks and limits credit usage |


---
# 1. Worksheets in Snowflake

## Scenario

After successfully helping Uncle Yer migrate his data into Snowflake, Tsai presents her findings to her team.

Today's topic is **Snowflake Worksheets**.

Worksheets are where developers:

- Write SQL
- Execute SQL
- Save queries
- Share code
- Review results

---

## What is a Worksheet?

A Worksheet is Snowflake's SQL editor.

It allows users to:

- Write SQL statements
- Execute queries
- View results
- Save scripts
- Share SQL with teammates

Think of it as the primary workspace for interacting with Snowflake.

---

## Creating Multiple Worksheets

A single project can contain multiple worksheets.

Example:

```
Project
├── Worksheet 1
│      SELECT * FROM ROOT_DEPTH;
│
├── Worksheet 2
│      SHOW TABLES;
│
└── Worksheet 3
       INSERT INTO ...
```

Each worksheet maintains its own configuration.

---

# 2. Worksheet Context

Every worksheet stores **four context settings**.

These determine where SQL executes and whether it has permission to run.

---

## Worksheet Context

```
Worksheet
│
├── Database
├── Schema
├── Role
└── Warehouse
```

---

## Database

Specifies the default database.

Example:

```
Database

GARDEN_PLANTS
```

Instead of writing:

```sql
SELECT *
FROM GARDEN_PLANTS.VEGGIES.ROOT_DEPTH;
```

you can simply write:

```sql
SELECT *
FROM ROOT_DEPTH;
```

because the worksheet already knows the default database.

---

## Schema

Specifies the default schema.

Example:

```
Schema

VEGGIES
```

Again, SQL becomes shorter because Snowflake already knows where to search.

---

## Role

Defines the permissions used when executing SQL.

Without a valid Role:

- Snowflake cannot determine whether you are authorized to access objects.

Example:

```
SYSADMIN
```

---

## Warehouse

Defines the compute resource used to execute SQL.

Without a Warehouse:

- Queries cannot run.

Example:

```
COMPUTE_WH
```

---

# 3. Required vs Optional Context

Not all context settings have the same purpose.

## Required Context

These are required for SQL execution:

- Role
- Warehouse

Without them:

- No permissions
- No compute
- Queries cannot execute

---

## Convenience Context

These are optional but highly recommended:

- Database
- Schema

They simply provide a default location for objects.

If omitted, fully qualified object names can be used instead.

Example:

```sql
SELECT *
FROM GARDEN_PLANTS.VEGGIES.ROOT_DEPTH;
```

---

## Why Are They Positioned Differently?

Snowflake places the context settings in different locations because they serve different purposes.

### Near the SQL Editor

- Database
- Schema

Purpose:

Provide convenience while writing SQL.

---

### Upper-Right Corner

- Role
- Warehouse

Purpose:

Required for query execution.

Without these, SQL cannot run.

---

# 4. Fully Qualified Object Names

Without Database and Schema context:

```sql
SELECT *
FROM ROOT_DEPTH;
```

fails because Snowflake does not know where to find the table.

Instead, specify the complete path.

```sql
SELECT *
FROM GARDEN_PLANTS.VEGGIES.ROOT_DEPTH;
```

General format:

```text
DATABASE.SCHEMA.OBJECT
```

---

# 5. First Rule of Troubleshooting

If Snowflake reports:

```
Table does not exist
```

or

```
Object does not exist
```

the **first thing to check is:**

> **Current Role**

Most "missing object" errors are actually permission problems.

---

# 6. What is a Warehouse?

Despite the name, a Snowflake Warehouse **does not store data**.

A Warehouse is a **compute engine**.

Its job is to perform:

- Query execution
- Data loading
- Data transformation
- Sorting
- Joins
- Aggregations
- Other computations

---

## Storage vs Compute

| Component | Purpose |
|------------|----------|
| Database | Stores data |
| Warehouse | Processes data |

---

## Easy Analogy

Think of Snowflake like this:

```
Database
    =
Hard Drive

Warehouse
    =
CPU
```

The database stores information.

The warehouse performs calculations.

---

# 7. Warehouse Architecture

A Warehouse consists of one or more **Clusters**.

Each Cluster contains multiple **Servers**.

```
Warehouse
│
└── Cluster
      ├── Server
      ├── Server
      ├── Server
      └── ...
```

---

## Cluster

A Cluster is simply a **group of servers** working together.

---

## Server

A Server performs the actual computation.

More servers provide more computing power.

---

# 8. Warehouse Sizes

Snowflake provides different warehouse sizes.

Example progression:

```
XS
S
M
L
XL
2XL
3XL
4XL
5XL
6XL
```

---

## Increasing Warehouse Size

Larger warehouses contain more servers.

Example:

```
XS
│
Few Servers
```

```
M
│
More Servers
```

The warehouse still contains **one cluster**, but that cluster has more servers.

---

# 9. Scaling Up and Down

Scaling **Up** means increasing warehouse size.

Example:

```
XS
▼
M
```

Result:

- More servers
- Faster processing
- Higher cost

---

Scaling **Down** means decreasing warehouse size.

Example:

```
XL
▼
M
```

Result:

- Fewer servers
- Lower cost
- Reduced processing power

---

## Summary

| Action | Meaning |
|----------|----------|
| Scale Up | Increase warehouse size |
| Scale Down | Decrease warehouse size |

---

# 10. Scaling Out and In

Scaling **Out** adds additional clusters.

Instead of making one cluster larger, Snowflake creates multiple clusters.

Example:

```
Warehouse

Cluster 1

↓

Cluster 1
Cluster 2
Cluster 3
```

This supports many users executing queries simultaneously.

---

## Scaling In

When demand decreases, Snowflake removes the extra clusters.

The course refers to this process as:

> **Snap Back**

```
High Demand

Cluster 1
Cluster 2
Cluster 3

↓

Demand Drops

↓

Cluster 1
```

---

## Summary

| Scaling Type | What Changes? |
|---------------|---------------|
| Scale Up | More servers in one cluster |
| Scale Down | Fewer servers in one cluster |
| Scale Out | More clusters |
| Scale In (Snap Back) | Extra clusters removed |

---

# 11. Auto Suspend and Auto Resume

The default trial warehouse (`COMPUTE_WH`) automatically manages itself.

## Auto Suspend

If no SQL runs for approximately **10 minutes**:

```
Warehouse

Running

↓

Idle

↓

Automatically Suspends
```

This saves Snowflake credits.

---

## Auto Resume

When a new query is submitted:

```
User Executes SQL

↓

Warehouse Automatically Starts

↓

Query Executes
```

No manual startup is required.

---

# 12. Warehouse Cost Best Practices

Larger warehouses consume more credits.

Example:

```
XS
↓

Low Cost
```

```
6XL
↓

Over 500× More Expensive
```

Snowflake recommends:

- Start with **XS**
- Increase size only when necessary

---

## General Recommendation

For most development work:

- XS
- Small

are sufficient.

Only scale up after confirming that additional compute is truly needed.

> [!important]
> Bigger warehouses are not automatically better. Choose the smallest warehouse that meets your workload requirements.

---

# 13. Resource Monitors

Resource Monitors help control warehouse spending.
![Pasted image 20260704160040](../Images/Pasted%20image%2020260704160040.png)
They can:

- Track credit usage
- Enforce usage limits
- Stop warehouses after limits are reached
- Send notifications

---

## Benefits

Resource Monitors protect against:

- Unexpected costs
- Accidental large warehouse usage
- Consuming all trial credits

---

## Notifications

Snowflake can notify users when usage approaches configured limits.
![Pasted image 20260704160051](../Images/Pasted%20image%2020260704160051.png)
Notifications can appear:

- Inside Snowflake
- Via email (if enabled)

---

## If a Resource Monitor Stops the Warehouse

Example message:

```
Warehouse cannot be resumed because
Resource Monitor quota has been exceeded.
```

Possible actions:

- Wait until the quota resets (e.g., next day).
- Increase the quota if appropriate.

Since the Resource Monitor belongs to your account, you have control over its configuration.

---

# Key Takeaways

- Worksheets are used to write, execute, save, and share SQL.
- Every worksheet stores four context settings:
  - Database
  - Schema
  - Role
  - Warehouse
- Role and Warehouse are required to execute SQL.
- Database and Schema act as convenient default locations.
- Fully qualified object names follow the format:
  `DATABASE.SCHEMA.OBJECT`
- Always check the current Role when troubleshooting "Object does not exist" errors.
- A Snowflake Warehouse is a compute engine, not a storage location.
- A Warehouse contains one or more Clusters, and each Cluster contains multiple Servers.
- Scaling Up/Down changes the number of servers in a cluster.
- Scaling Out/In adds or removes clusters (also called ==**Snap Back**== when clusters are removed).
- Auto Suspend and Auto Resume reduce unnecessary credit consumption.
- Start with an XS warehouse and scale up only when justified.
- Resource Monitors help control costs and prevent excessive credit usage.

---

