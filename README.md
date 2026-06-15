# Chapter 1: Entity Relationship Diagram (ERD)

## Definition

An **Entity Relationship Diagram (ERD)** is a graphical representation of data requirements and relationships in a database.

### Purpose

* Identify data to be stored
* Support business activities
* Generate reports and performance measures
* Show relationships between data

---

## Main Components

### 1. Entity
A person, place, object, or thing about which data is stored.

### 2. Attribute
A characteristic that describes an entity.

### 3. Relationships
A relationship is an association between entities.

---

## Relationship Types

### One-to-One (1:1)

One occurrence of an entity is associated with one occurrence of another entity.

Example:

Manager ↔ Department

Rules:

* One department has at most one manager.
* One manager heads at most one department.

---

### One-to-Many (1:M)

One occurrence of an entity is associated with many occurrences of another entity.

Example:

Manager → Employee

Rules:

* One manager supervises many employees.
* One employee has one manager.

---

### Many-to-Many (M:N)

Many occurrences of one entity are associated with many occurrences of another entity.

Example:

Employee ↔ Project

Rules:

* One employee can work on many projects.
* One project can have many employees.

---

# Chapter 2: Enhanced Entity Relationship Model (EER)

## Why EER?

Basic ER modelling cannot represent complex business rules effectively.

The **Enhanced Entity Relationship Model (EER)** extends ER modelling by adding more semantic meaning.

An EER diagram is called an **EERD**.

---

## Additional Features of EER

* Supertypes
* Subtypes
* Inheritance
* Specialization
* Generalization
* Additional business rules

---

## Connection Traps

Connection traps occur when relationships are interpreted incorrectly.

### Fan Trap

A relationship path exists but is ambiguous.

```text
A → B → C
```

Cannot clearly determine the relationship between A and C.

---

### Chasm Trap

A relationship appears to exist, but some records have no valid path.

```text
A → B → C
```

Some B records do not connect to C.

---

## Supertype

A general entity containing common attributes.

Example:

```text
Person
```

---

## Subtype

A specialized entity that inherits attributes from a supertype.

Examples:

```text
Student
Employee
```

---

## Inheritance

A subtype automatically inherits attributes from its supertype.

Example:

```text
Person
 ├─ Student
 └─ Employee
```

Student and Employee inherit Person attributes.

---

## Specialization

Process of dividing a supertype into subtypes.

Example:

```text
Employee
 ├─ Manager
 └─ Engineer
```

General → Specific

---

## Generalization

Process of combining subtypes into a supertype.

Example:

```text
Manager
Engineer
    ↓
 Employee
```

Specific → General

---

## Subtype Constraints

### Disjoint

An entity can belong to only one subtype.

Example:

A person can be either:

* Manager
* Engineer

but not both.

---

### Overlapping

An entity can belong to multiple subtypes.

Example:

A person can be:

* Employee
* Student

at the same time.

---

### Total Participation

Every supertype occurrence must belong to a subtype.

---

### Partial Participation

A supertype occurrence may belong to no subtype.

---

## Chapter Summary

### Key Concepts

| Concept        | Meaning                          |
| -------------- | -------------------------------- |
| Supertype      | Parent entity                    |
| Subtype        | Child entity                     |
| Inheritance    | Child receives parent attributes |
| Specialization | Split                            |
| Generalization | Merge                            |
| Disjoint       | One subtype only                 |
| Overlapping    | Multiple subtypes allowed        |
| Total          | Must belong to subtype           |
| Partial        | May belong to none               |

### Memory Aid

```text
Specialization = Split
Generalization = Merge

Supertype = Parent
Subtype = Child

Inheritance = Child gets parent's attributes
```
---

# Chapter 5: Stored Procedures

## Definition

A **Stored Procedure** is a collection of SQL statements stored in the database and executed as a single unit.

Think of it as a **saved SQL program** that can be executed whenever needed.

---

## Advantages of Stored Procedures

### 1. Reusability

Write once and execute many times.

### 2. Security

Users can execute procedures without direct access to underlying tables.

### 3. Better Performance

Execution plans are stored and reused by the DBMS.

### 4. Reduced Network Traffic

Instead of sending multiple SQL statements, only one procedure call is sent.

### 5. Consistency

All users execute the same business logic.

---

# Chapter 6: Integrity Constraints and Triggers

# Integrity Constraints

Integrity constraints ensure database data remains accurate and consistent.

---

## Types of Integrity Constraints

### 1. Required Data

Ensures a column cannot contain NULL values.

```sql
NOT NULL
```

Example:

```sql
position VARCHAR(50) NOT NULL
```

---

### 2. Domain Constraints

Restrict valid values that can be stored.

Example:

```sql
CHECK (gender IN ('M','F'))
```

Other examples:

```sql
CHECK(age > 0)

CHECK(salary >= 0)
```

---

### 3. Entity Integrity

Ensures each row can be uniquely identified.

### Primary Key Rules

* Must be unique
* Cannot be NULL

Example:

```sql
PRIMARY KEY(staffNo)
```

### Composite Primary Key

```sql
PRIMARY KEY(clientNo, propertyNo)
```

### Alternate Key

A unique column that is not the primary key.

```sql
UNIQUE(telNo)
```

---

### 4. Referential Integrity

Maintains relationships between tables.

### Foreign Key

```sql
FOREIGN KEY(branchNo)
REFERENCES Branch(branchNo)
```

Foreign key values must exist in the parent table.

---

## Referential Actions

### CASCADE

```sql
ON DELETE CASCADE
```

Deleting parent automatically deletes child records.

---

### SET NULL

```sql
ON DELETE SET NULL
```

Foreign key becomes NULL.

---

### SET DEFAULT

```sql
ON DELETE SET DEFAULT
```

Foreign key becomes default value.

---

### NO ACTION

```sql
ON DELETE NO ACTION
```

Deletion is rejected if child records exist.

---

### 5. Enterprise Constraints

Business rules specific to an organization.

Examples:

* Manager salary ≤ 30000
* Staff manages ≤ 100 properties

Often implemented using triggers.

---

# Triggers

## Definition

A **Trigger** is a special stored procedure that executes automatically when a specified event occurs.

### Difference from Stored Procedures

| Stored Procedure  | Trigger                |
| ----------------- | ---------------------- |
| Executed manually | Executed automatically |

---

## Uses of Triggers

* Enforce business rules
* Maintain integrity
* Record audit information
* Prevent invalid operations
* Update related tables automatically

---

## Trigger Categories

### DML Triggers

Respond to:

```sql
INSERT
UPDATE
DELETE
```

---

### DDL Triggers

Respond to:

```sql
CREATE
ALTER
DROP
```

---

### Logon Triggers

Respond when users log in.

---

## Chapter Summary

### Integrity Constraints

| Type                  | SQL Mechanism |
| --------------------- | ------------- |
| Required Data         | NOT NULL      |
| Domain Constraint     | CHECK         |
| Entity Integrity      | PRIMARY KEY   |
| Referential Integrity | FOREIGN KEY   |
| Enterprise Constraint | Trigger       |

### Trigger Types

| Trigger      | Fires When      |
| ------------ | --------------- |
| AFTER INSERT | After insert    |
| AFTER UPDATE | After update    |
| AFTER DELETE | After delete    |
| INSTEAD OF   | Replaces action |

---

# Chapter 7: Database Administration (DA & DBA)

## Introduction

A DBMS alone does not guarantee a successful information system.

Effective database administration requires:

* Technology
* Management
* User acceptance

---

## Database Administration Aspects

| Aspect        | Description             |
| ------------- | ----------------------- |
| Technological | Hardware and DBMS       |
| Managerial    | Planning and management |
| Cultural      | Employee acceptance     |

---

## Data Administrator (DA)

### Definition

Responsible for organization-wide management of data resources.

### Focus

* Policies
* Standards
* Planning
* Security strategies

### Responsibilities

* Set data goals
* Create policies
* Create standards
* Long-term planning
* Conceptual database design
* Logical database design

---

## Database Administrator (DBA)

### Definition

Responsible for technical database management.

### Focus

* Operations
* Security
* Performance
* Backup and recovery

### Responsibilities

* Physical database design
* Database control
* User support
* Security implementation
* Backup and recovery
* Authorization management
* Performance tuning

---

## Main DBA Duties

### DBMS Selection

Consider:

* Cost
* Security
* Performance
* Storage
* Vendor support

---

### End User Support

* Training
* Problem solving
* Requirement gathering

---

### Security

* Passwords
* Encryption
* Firewalls
* Access privileges

---

### Backup and Recovery

* Regular backups
* Backup identification
* Multiple backup locations

---

### Authorization Management

Control:

* Users
* Groups
* Privileges
* Views

---

## DA vs DBA (Important)

| Area     | DA                   | DBA            |
| -------- | -------------------- | -------------- |
| Focus    | Managerial           | Technical      |
| Scope    | Organization-wide    | DBMS-specific  |
| Planning | Long-term            | Short-term     |
| Design   | Conceptual & Logical | Physical       |
| Policies | Creates              | Enforces       |
| Security | Strategic planning   | Implementation |

---

## Memory Aid

```text
DA = Decide

Policies
Standards
Planning

DBA = Do

Security
Backup
Recovery
Performance
Operations
```

---

# Chapter 8: Database Security

## Definition

Database security protects:

* Data
* DBMS software
* Hardware
* Networks
* Users
* Backup systems

---

## Importance

Poor security can cause:

* Financial loss
* Legal issues
* Reputation damage
* Business disruption

---

## Database Threats

### Theft and Fraud

Unauthorized access or manipulation of data.

### Loss of Confidentiality

Sensitive data becomes visible to unauthorized users.

### Loss of Privacy

Personal information is exposed.

### Loss of Integrity

Data is modified incorrectly.

### Loss of Availability

Users cannot access the database.

Causes:

* Hardware failure
* System crash
* Denial of Service attacks

---

## Authentication vs Authorization

### Authentication

Verifies identity.

Examples:

* Username/password
* Biometrics

Question:

> Who are you?

---

### Authorization

Determines permitted actions.

Examples:

* SELECT
* INSERT
* UPDATE
* DELETE

Question:

> What can you do?

---

## Access Control

Determines:

* Who can access data
* What data they can access
* What operations they can perform

---

## Authorization Components

### Users

People accessing the database.

### Objects

Database items being protected.

Examples:

* Tables
* Columns
* Rows

### Privileges

Allowed actions.

Examples:

* SELECT
* INSERT
* UPDATE
* DELETE

---

## Types of Security

### User-Based Security

Permissions assigned to users.

### Object-Based Security

Permissions assigned to database objects.

---

## GRANT

Used to give permissions.

### Syntax

```sql
GRANT action
ON object
TO user;
```

Example:

```sql
GRANT SELECT, INSERT
ON employees
TO Smith;
```

---

### WITH GRANT OPTION

Allows a user to grant permissions to others.

```sql
GRANT SELECT
ON employees
TO Smith
WITH GRANT OPTION;
```

---

### Column-Level Permissions

```sql
GRANT UPDATE(price)
ON products
TO Jones;
```

---

## REVOKE

Used to remove permissions.

### Syntax

```sql
REVOKE action
ON object
FROM user;
```

Example:

```sql
REVOKE SELECT
ON employees
FROM Smith;
```

---

## Chapter Summary

### Security Concepts

| Concept        | Meaning                 |
| -------------- | ----------------------- |
| Authentication | Identity verification   |
| Authorization  | Permission verification |

### SQL Security Commands

| Command | Purpose            |
| ------- | ------------------ |
| GRANT   | Give permissions   |
| REVOKE  | Remove permissions |

### Memory Aid

```text
Authentication = Who are you?
Authorization = What can you do?

GRANT = Give access
REVOKE = Remove access
```

---

# Chapter 9: Transactions, Concurrency Control & Recovery

## Transaction

A **transaction** is a sequence of database operations treated as a single unit of work.

Examples:

* Transfer money between accounts
* Update inventory after a sale
* Place an order

### Transaction Outcomes

#### Commit

Transaction completes successfully.

* Changes become permanent.
* Database reaches a new consistent state.

#### Rollback (Abort)

Transaction fails.

* All changes are undone.
* Database returns to its previous state.

---

# ACID Properties

Transactions must satisfy the ACID properties.

### Atomicity

"All or Nothing"

* Entire transaction succeeds, or
* Entire transaction fails

---

### Consistency

* Database moves from one valid state to another.
* Constraints and rules remain satisfied.

---

### Isolation

* Transactions should not interfere with one another.
* Each transaction behaves as if it is running alone.

---

### Durability

* Once committed, changes are permanent.
* Data survives crashes and failures.

---

## Concurrency Control

Concurrency control manages multiple transactions executing simultaneously.

### Goals

* Improve performance
* Maintain correctness
* Prevent conflicts

---

# Concurrency Problems

## 1. Lost Update

Two transactions update the same data.

Example:

```text
Balance = 100

T1 adds 50 → 150
T2 adds 20 → 120

Final balance = 120 ❌
Expected = 170
```

---

## 2. Dirty Read (Uncommitted Dependency)

A transaction reads uncommitted data.

```text
T1 changes value to 200
T2 reads 200

T1 rolls back

T2 used invalid data
```

---

## 3. Inconsistent Analysis

A transaction reads data while another transaction is updating it.

Result:

* Mixed old and new values
* Incorrect calculations

---

# Schedules

## Serial Schedule

Transactions execute one after another.

```text
T1 → T2 → T3
```

Advantages:

* Safe
* No conflicts

Disadvantage:

* Slow

---

## Non-Serial Schedule

Transactions are interleaved.

```text
T1 Read
T2 Read
T1 Write
T2 Write
```

Advantages:

* Better performance

Disadvantage:

* May cause conflicts

---

# Serializability

A schedule is **serializable** if it produces the same result as a serial schedule.

### Goal

Allow concurrency while preserving correctness.

---

# Locking

The most common concurrency-control technique.

Transactions lock data before accessing it.

---

## Shared Lock (S)

Used for reading.

Characteristics:

* Multiple transactions may read.
* No updates allowed.

---

## Exclusive Lock (X)

Used for writing.

Characteristics:

* Only one transaction allowed.
* Read and write permitted.

---

# Two-Phase Locking (2PL)

Guarantees serializability.

### Phase 1: Growing Phase

* Acquire locks only.
* Cannot release locks.

### Phase 2: Shrinking Phase

* Release locks only.
* Cannot acquire new locks.

---

### Advantages

* Ensures correctness
* Guarantees serializability

### Disadvantages

* Can cause deadlocks
* Reduces concurrency

---

# Timestamping

Each transaction receives a timestamp.

Transactions execute according to timestamp order.

Advantages:

* No locks required

---

# Optimistic Concurrency Control

Assumes conflicts are rare.

Process:

1. Execute transaction
2. Validate at commit
3. Commit or rollback

Advantages:

* High performance when conflicts are rare

---

# Recovery

Recovery restores the database after failure.

---

## Causes of Failure

* System crash
* Power failure
* Hardware failure
* Software errors
* Human mistakes
* Natural disasters

---

# Storage Types

## Volatile Storage

Examples:

* RAM

Characteristics:

* Data lost after crash

---

## Non-Volatile Storage

Examples:

* Hard disks
* SSDs

Characteristics:

* Data survives crashes

---

# Recovery Actions

## Undo (Rollback)

Removes effects of incomplete transactions.

---

## Redo (Rollforward)

Reapplies committed transactions not yet written to disk.

---

# Logging

A log records database changes.

Typically stores:

* Transaction ID
* Operation
* Before Image
* After Image

Example:

```text
T1 UPDATE Balance

Before: 100
After : 150
```

---

# Checkpoint

A checkpoint is a save point in the database.

Purpose:

* Reduce recovery time
* Mark a consistent state

---

## Recovery Using Checkpoints

After a crash:

### Redo

Committed transactions after checkpoint.

### Undo

Incomplete transactions at crash time.

---

# Chapter Summary

## ACID

| Property    | Meaning                |
| ----------- | ---------------------- |
| Atomicity   | All or nothing         |
| Consistency | Valid state maintained |
| Isolation   | No interference        |
| Durability  | Permanent after commit |

---

## Concurrency Problems

* Lost Update
* Dirty Read
* Inconsistent Analysis

---

## Control Techniques

* Locking
* Two-Phase Locking (2PL)
* Timestamping
* Optimistic Control

---

## Recovery Tools

* Logs
* Checkpoints
* Undo
* Redo

---

# Chapter 10: Normalization, Denormalization & Partitioning

# Normalization

Normalization organizes database tables to:

* Reduce redundancy
* Improve consistency
* Eliminate update anomalies

---

## Benefits

* Cleaner design
* Less duplicate data
* Easier maintenance

---

## Drawbacks

Highly normalized databases may:

* Require many tables
* Require many JOIN operations
* Reduce query performance

---

# Denormalization

Denormalization intentionally introduces redundancy to improve performance.

---

## Purpose

Improve query speed, especially for read-heavy systems.

---

## Advantages

* Faster data retrieval
* Fewer joins
* Better reporting performance

---

## Disadvantages

* More duplicate data
* Increased storage requirements
* Higher maintenance effort
* Greater risk of inconsistency

---

## When to Use

Suitable when:

* Read performance is critical
* Reporting is frequent
* Real-time queries are important

---

# Common Denormalization Techniques

### 1. Combine 1:1 Tables

Merge related tables into one.

---

### 2. Duplicate Attributes

Copy frequently used attributes.

---

### 3. Duplicate Foreign Keys

Store foreign keys in multiple locations.

---

### 4. Repeating Groups

Store multiple values within a row.

(Not recommended in fully normalized systems.)

---

# Partitioning

Partitioning splits data into smaller pieces to improve performance and manageability.

---

## Horizontal Partitioning

Split a table by rows.

Example:

```text
Customer_Malaysia
Customer_Singapore
Customer_Thailand
```

Characteristics:

* Same columns
* Different rows

---

## Vertical Partitioning

Split a table by columns.

Example:

```text
CustomerBasic
CustomerFinancial
```

Characteristics:

* Same rows
* Different columns

---

# Comparison

| Concept         | Purpose                               |
| --------------- | ------------------------------------- |
| Normalization   | Reduce redundancy                     |
| Denormalization | Improve performance                   |
| Partitioning    | Improve performance and manageability |

---

# Denormalization Summary

| Advantages           | Disadvantages         |
| -------------------- | --------------------- |
| Faster retrieval     | Slower updates        |
| Fewer joins          | More redundancy       |
| Better reporting     | Higher storage use    |
| Improved performance | Risk of inconsistency |

---

# Chapter Summary

```text
Normalization
→ Reduce redundancy

Denormalization
→ Add redundancy for speed

Partitioning
→ Split data for performance
```

---

# Chapter 11: Data Warehouse

## Definition

A **Data Warehouse** is a database designed for:

* Analysis
* Reporting
* Decision support

It is separate from operational databases.

---

# Characteristics (Inmon Definition)

A data warehouse is:

1. Subject-Oriented
2. Integrated
3. Time-Variant
4. Non-Volatile

---

## 1. Subject-Oriented

Organized around business subjects.

Examples:

* Customers
* Products
* Sales

---

## 2. Integrated

Data comes from multiple sources.

Examples:

* Operational databases
* Excel files
* External systems

Data is cleaned and standardized.

---

## 3. Time-Variant

Stores historical data.

Used for:

* Trend analysis
* Performance analysis
* Forecasting

---

## 4. Non-Volatile

Data is mostly:

* Loaded
* Queried

Not frequently updated or deleted.

---

# Purpose of a Data Warehouse

Used for:

* Business analysis
* Strategic planning
* Decision making

---

## Examples

### Customer Analysis

* Buying habits
* Spending patterns
* Customer behavior

### Product Analysis

* Sales trends
* Product performance
* Regional performance

---

# OLTP vs OLAP

| Feature | OLTP              | OLAP              |
| ------- | ----------------- | ----------------- |
| Purpose | Transactions      | Analysis          |
| Users   | Staff             | Managers/Analysts |
| Data    | Current           | Historical        |
| Queries | Simple            | Complex           |
| Focus   | Fast transactions | Fast analysis     |
| Usage   | Daily operations  | Decision support  |

---

## Easy Memory

```text
OLTP = Run Business

OLAP = Analyze Business
```

---

# Data Warehouse Architecture

Data is collected from multiple sources and processed using ETL.

### ETL Process

1. Extract
2. Transform
3. Load

---

# Data Cube

A multidimensional model used in data warehouses.

---

## Dimensions

Examples:

* Time
* Product
* Region

---

## Measures

Examples:

* Sales Amount
* Quantity Sold

---

# Fact Table

Central table containing measurable data.

Examples:

* Sales Amount
* Quantity Sold

---

# Dimension Tables

Provide descriptive information.

Examples:

### Product

* Product Name
* Brand
* Category

### Time

* Day
* Month
* Year

### Location

* City
* Region

---

# Schema Types

## Star Schema

Most common design.

Characteristics:

* One fact table
* Multiple dimension tables

Advantages:

* Simple
* Fast queries

---

## Snowflake Schema

Normalized version of Star Schema.

Advantages:

* Less redundancy

Disadvantages:

* More joins
* More complex

---

## Fact Constellation (Galaxy Schema)

Contains:

* Multiple fact tables
* Shared dimension tables

---

# Advantages of Data Warehouses

* Better decision making
* Historical analysis
* Trend identification
* Business intelligence support

---

# Chapter Summary

## Data Warehouse Characteristics

| Characteristic   | Meaning                       |
| ---------------- | ----------------------------- |
| Subject-Oriented | Organized by business subject |
| Integrated       | Combines multiple sources     |
| Time-Variant     | Historical data               |
| Non-Volatile     | Mostly read-only              |

---

## Schema Types

| Schema             | Description                 |
| ------------------ | --------------------------- |
| Star               | One fact table + dimensions |
| Snowflake          | Normalized dimensions       |
| Fact Constellation | Multiple fact tables        |

---

## Memory Aid

```text
Data Warehouse

Subject-Oriented
Integrated
Time-Variant
Non-Volatile

OLTP = Transactions
OLAP = Analysis

ETL
Extract
Transform
Load
```

---

