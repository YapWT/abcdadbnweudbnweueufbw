# Chap1
Entity Relationship Diagram (ERD)
An Entity Relationship Diagram (ERD) is a graphical representation of an organization's data requirements. It provides a high-level, conceptual view of a database structure and helps model the **data view** of a system.

ERDs are used to:

* Identify the data that must be captured, stored, and retrieved.
* Support business activities within an organization.
* Identify data needed for reports and performance measurements.
* Show how data is related within a database.

An ERD consists of three main components:

* **Entities**
* **Attributes**
* **Relationships**

---

### Entities

An entity is a person, place, object, or thing about which data is stored.

Anything that an organization needs to keep information about can be considered an entity.

Examples:

* Customer
* Employee
* Student
* Supplier
* Book
* Invoice
* Vehicle

An entity must be uniquely identifiable.

Examples:

* If a bank stores information about a customer, the customer is an entity.
* If a library stores information about a book, the book is an entity.
* If a company stores information about an invoice, the invoice is an entity.

---

### Attributes

Attributes are the pieces of information that describe an entity.

They are the smallest meaningful units of data associated with an entity.

Example:

**Supplier**

Attributes:

* Supplier_ID
* Supplier_Name
* Supplier_Address

Example:

**Student**

Attributes:

* Student_ID
* Name
* Date_of_Birth
* Email

---

### Identifying Entities and Attributes

A common technique is to look for nouns in a business description.

Ask:

> Is the organization likely to store data about this?

If yes, it is probably an **entity**.

If it only describes an entity, it is probably an **attribute**.

Example:

> Each engineer is allocated one van (which is driven up to a certain mileage and then replaced). Each member has only one address but perhaps many vehicles. Each visit is to deal with only one vehicle. A member can be visited more than once on any given date and there may be many visits to a member on different dates. A member may only be covered for some of the vehicles they own and not for others.

Nouns:

* Engineer
* Van
* Mileage
* Member
* Address
* Vehicle
* Visit
* Date

Entities:

* Engineer
* Van
* Member
* Vehicle
* Visit

Attributes:

* Mileage (Van)
* Address (Member)
* Date (Visit)

---

### Relationships

A relationship is an association between two or more entities.

Examples:

* PLAYER plays for TEAM
* PERSON is a citizen of COUNTRY
* EMPLOYEE works in DEPARTMENT
* LAWYER advises CLIENT
* EQUIPMENT is allocated to PROJECT

---

### One-to-One Relationship (1:1)

A single occurrence of one entity is related to only one occurrence of another entity.

Example:

MANAGER — HEAD OF — DEPARTMENT

Rules:

* One department has at most one manager.
* One manager heads at most one department.

Representation:

```text
[Manager] ----1:1---- [Department]
```

---

### One-to-Many Relationship (1:M)

One occurrence of an entity can be related to many occurrences of another entity.

Example:

MANAGER — SUPERVISES — EMPLOYEE

Rules:

* One manager can supervise many employees.
* One employee is supervised by only one manager.

Representation:

```text
[Manager] ----1:M---- [Employee]
```

---

### Many-to-Many Relationship (M:N)

Many occurrences of one entity can be related to many occurrences of another entity.

Example:

EMPLOYEE — ASSIGNED TO — PROJECT

Rules:

* One employee can work on many projects.
* One project can have many employees.

Representation:

```text
[Employee] ----M:N---- [Project]
```

---

### Resolving Many-to-Many Relationships

Relational databases cannot directly support M:N relationships.

A **link entity** (also called an associative entity) must be introduced.

Example:

A supplier can supply many parts.

A part can be supplied by many suppliers.

Original relationship:

```text
[Supplier] ----M:N---- [Part]
```

After decomposition:

```text
[Supplier] ----1:M---- [Supplier_Part] ----M:1---- [Part]
```

The new entity (**Supplier_Part**) acts as a link between Supplier and Part.

---

### ERD Symbols

**Entity**

Represented by a rectangle.

```text
+-----------+
| Student   |
+-----------+
```

**Relationship**

Represented by a labeled line connecting entities.

```text
[Student] ---- Enrolled In ---- [Course]
```

---

### Steps to Create an ERD

1. Identify likely entities from the business description.
2. Select a unique identifier (primary key) for each entity.
3. Create an entity relationship grid.
4. Identify relationships between entities.
5. Determine the relationship type:

   * 1:1
   * 1:M
   * M:N
6. Draw the ERD.
7. If an M:N relationship exists, create a link entity and redraw the ERD.

---
# Chap 2

Enhanced Entity Relationship Model (EER) 



ER Modelling is a useful tool for designing relational databases because it helps represent entities, attributes, and relationships.



However, basic ER modelling has some limitations:



* Provides semantic (meaningful) information, but not always enough.

* Difficult to represent more complex business rules.

* May lead to misunderstanding of relationships.



Database development process:



```text

Requirements Definition

          ↓

     Data Analysis

          ↓

 Conceptual Data Model

          ↓

   Logical Data Model

          ↓

    Physical Design

          ↓

       Database

```



---



## Connection Traps



Connection traps occur when relationships in an ER model are interpreted incorrectly.



Two common types:



1. Fan Trap

2. Chasm Trap



---



## Fan Trap



A fan trap happens when a model suggests a relationship exists, but the path between entities is ambiguous.



### Example



```text

Department

    |

   1:M

    |

 Employee

    |

   1:M

    |

 Project

```



Question:



> Which projects belong to a department?



The model seems to suggest a department is related to projects through employees.



However:



* Employees belong to departments.

* Employees work on projects.



There is no direct relationship between Department and Project.



The path is ambiguous.



### Visual



```text

[Department]

      |

     1:M

      |

[Employee]

      |

     1:M

      |

[Project]

```



Problem:



* Different employees in the same department may work on different projects.

* We cannot accurately determine all projects of a department.



---



## Chasm Trap



A chasm trap occurs when the model suggests a relationship exists, but for some records the relationship path does not exist.



### Example



```text

Branch

   |

 1:M

   |

 Staff

   |

 0:M

   |

 Property

```



Not every staff member manages a property.



Question:



> Which properties belong to a branch?



Some staff members may not manage any properties.



This creates a gap (chasm) in the relationship path.



### Visual



```text

[Branch]

    |

   1:M

    |

 [Staff]

    |

   0:M

    |

[Property]

```



Problem:



* Some branch records cannot reach property records.

* The relationship is incomplete.



---



# Enhanced ER Model (EER)



To overcome limitations of ER modelling, the Enhanced Entity Relationship Model (EER) was introduced.



A diagram created using EER is called an:



**EERD (Enhanced Entity Relationship Diagram)**



EER adds:



* Supertypes

* Subtypes

* Inheritance

* Specialization

* Generalization

* Additional business rules



---



# Supertype and Subtype



## Supertype



A supertype is a general entity that contains attributes shared by multiple entity types.



### Example



```text

Person

```



Common attributes:



* Person_ID

* Name

* Address



---



## Subtype



A subtype is a more specific version of a supertype.



It contains:



* All attributes inherited from the supertype.

* Additional attributes unique to that subtype.



### Example



```text

                Person

                   |

         -------------------

         |                 |

      Student          Employee

```



Student attributes:



* Student_ID

* Course



Employee attributes:



* Salary

* Position



---



## IS-A Relationship



Subtype and supertype relationships are often called **IS-A relationships**.



Example:



```text

Student IS A Person

Employee IS A Person

```



Visual:



```text

          Person

             |

      ----------------

      |              |

   Student       Employee

```



---



# Attribute Inheritance



Subtypes automatically inherit attributes from the supertype.



Example:



```text

Person

------

Person_ID

Name

Address

```



Student inherits:



```text

Student

-------

Person_ID

Name

Address

Course

```



Employee inherits:



```text

Employee

--------

Person_ID

Name

Address

Salary

```



### Important Rule



All subtypes inherit the primary key of the supertype.



---



# Subtype Discriminator



A subtype discriminator is an attribute in the supertype that determines which subtype an entity belongs to.



Example:



```text

Person

------

Person_ID

Name

Person_Type

```



Person_Type values:



| Person_Type | Subtype  |

| ----------- | -------- |

| Student     | Student  |

| Employee    | Employee |



Visual:



```text

             Person

      (Person_Type)

                 |

        ----------------

        |              |

     Student      Employee

```



Usually based on equality comparison.



Example:



```text

IF Person_Type = 'Student'

THEN Student subtype

```



---



# Disjoint and Overlapping Constraints



## Disjoint Subtypes



Also called non-overlapping subtypes.



An entity occurrence can belong to only ONE subtype.



Example:



```text

          Person

             |

      ----------------

      |              |

   Student      Employee

```



Rule:



A person is either:



* Student



OR



* Employee



Not both.



Visual:



```text

Person

  |

[D]

  |

---------

|       |

Student Employee

```



(D = Disjoint)



---



## Overlapping Subtypes



An entity occurrence can belong to multiple subtypes.



Example:



```text

          Person

             |

      ----------------

      |              |

   Student      Employee

```



Rule:



A person may be:



* Student only

* Employee only

* Both Student and Employee



Visual:



```text

Person

  |

[O]

  |

---------

|       |

Student Employee

```



(O = Overlapping)



---



# Completeness Constraints



Shows whether every supertype occurrence must belong to a subtype.



Two types:



* Total

* Partial



---



## Total Completeness



Every supertype instance must belong to at least one subtype.



Example:



```text

Employee

    |

    |

-------------

|           |

Manager   Engineer

```



Every employee must be:



* Manager OR

* Engineer



Visual:



```text

Employee

    ||

-------------

|           |

Manager   Engineer

```



(Double line = Total)



---



## Partial Completeness



Some supertype instances may not belong to any subtype.



Example:



```text

Person

   |

---------

|       |

Student Employee

```



A person may be:



* Student

* Employee

* Neither



Visual:



```text

Person

    |

---------

|       |

Student Employee

```



(Single line = Partial)



---



# Specialization



Specialization is a **top-down approach**.



Start with a general supertype and create more specific subtypes.



### Example



Start:



```text

Employee

```



Create:



```text

Employee

    |

------------------

|                |

Manager      Engineer

```



Reason:



* Managers have special responsibilities.

* Engineers have technical skills.



General → Specific



---



# Generalization



Generalization is a **bottom-up approach**.



Start with several entities and combine them into a common supertype.



### Example



Start:



```text

Student

Employee

```



Identify common attributes:



* Name

* Address

* ID



Create:



```text

          Person

             |

      ----------------

      |              |

   Student      Employee

```



Specific → General



---



# Comparison: Specialization vs Generalization



| Specialization           | Generalization        |

| ------------------------ | --------------------- |

| Top-down                 | Bottom-up             |

| Start with supertype     | Start with subtypes   |

| Create specific entities | Create generic entity |

| General → Specific       | Specific → General    |



Example:



```text

Specialization



Employee

    |

------------------

|                |

Manager      Engineer

```



```text

Generalization



Manager     Engineer

      \      /

       \    /

      Employee

```



---



# Exam Tips



### Fan Trap



Remember:



> Relationship exists but the path is ambiguous.



```text

A → B → C

```



Cannot clearly determine A ↔ C.



---



### Chasm Trap



Remember:



> Relationship appears to exist but some records have no path.



```text

A → B → C

```



Some B records do not connect to C.



---



### Supertype



General entity containing common attributes.



Example:



```text

Person

```



---



### Subtype



Specific entity inheriting from a supertype.



Example:



```text

Student

Employee

```



---



### Specialization



```text

Employee

    ↓

Manager, Engineer

```



General → Specific



---



### Generalization



```text

Manager + Engineer

        ↓

     Employee

```



Specific → General



---



### Easy Memory Trick



```text

Specialization = Split



Employee

   ↓

Manager

Engineer

```



```text

Generalization = Merge



Manager

Engineer

   ↓

Employee

```



```text

Supertype = Parent

Subtype = Child

Inheritance = Child gets parent's attributes

Disjoint = One subtype only

Overlapping = Multiple subtypes allowed

Total = Must belong to a subtype

Partial = May belong to no subtype

```
---
# Chap 3

## What is SQL?

**SQL (Structured Query Language)** is the standard language used to interact with databases.

A database language should allow users to:

* Create databases and tables.
* Insert data.
* Update data.
* Delete data.
* Retrieve data using queries.

SQL has 3 major components:

| Component                        | Purpose                        |
| -------------------------------- | ------------------------------ |
| DDL (Data Definition Language)   | Define database structure      |
| DML (Data Manipulation Language) | Retrieve and modify data       |
| DCL (Data Control Language)      | Control access and permissions |

Examples:

```sql
CREATE TABLE Staff (
    staffNo VARCHAR(5),
    lName VARCHAR(15),
    salary DECIMAL(7,2)
);
```

```sql
INSERT INTO Staff
VALUES ('SG16', 'Brown', 8300);
```

```sql
SELECT staffNo, lName, salary
FROM Staff
WHERE salary > 10000;
```

---

# SELECT Statement

General structure:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

Syntax:

```sql
SELECT [DISTINCT | ALL] columnList
FROM tableName
[WHERE condition]
[GROUP BY columnList]
[HAVING condition]
[ORDER BY columnList];
```

Purpose of each clause:

| Clause   | Purpose            |
| -------- | ------------------ |
| SELECT   | Columns to display |
| FROM     | Table(s) used      |
| WHERE    | Filter rows        |
| GROUP BY | Create groups      |
| HAVING   | Filter groups      |
| ORDER BY | Sort output        |

### Important

* Order cannot be changed.
* Only **SELECT** and **FROM** are mandatory.

---

# DISTINCT

Removes duplicate values.

Without DISTINCT:

```sql
SELECT propertyNo
FROM Viewing;
```

With DISTINCT:

```sql
SELECT DISTINCT propertyNo
FROM Viewing;
```

---

# Calculated Columns

Can perform calculations in SELECT.

Example:

```sql
SELECT staffNo, fName, lName, salary/12
FROM Staff;
```

Rename using AS:

```sql
SELECT staffNo, fName, lName,
       salary/12 AS monthlySalary
FROM Staff;
```

---

# WHERE Clause

Used to filter rows.

Example:

```sql
SELECT *
FROM Staff
WHERE salary > 10000;
```

---

# Logical Operators

### OR

```sql
SELECT *
FROM Branch
WHERE city = 'London'
   OR city = 'Glasgow';
```

---

### AND

```sql
SELECT *
FROM Staff
WHERE salary > 10000
AND position = 'Manager';
```

---

# BETWEEN

Used for ranges.

```sql
SELECT *
FROM Staff
WHERE salary BETWEEN 20000 AND 30000;
```

Equivalent to:

```sql
WHERE salary >= 20000
AND salary <= 30000
```

### Notes

* Includes both endpoints.
* Has NOT BETWEEN version.

---

# IN

Used when checking multiple values.

```sql
SELECT *
FROM Staff
WHERE position IN ('Manager','Supervisor');
```

Equivalent to:

```sql
WHERE position='Manager'
OR position='Supervisor'
```

### Notes

* Has NOT IN version.
* More efficient when many values are involved.

---

# LIKE

Used for pattern matching.

```sql
SELECT *
FROM PrivateOwner
WHERE address LIKE '%Glasgow%';
```

Special symbols:

| Symbol | Meaning                 |
| ------ | ----------------------- |
| %      | Zero or more characters |
| _      | Exactly one character   |

Examples:

```sql
LIKE '%Glasgow%'
```

Contains Glasgow anywhere.

```sql
LIKE 'A%'
```

Starts with A.

```sql
LIKE '_ohn'
```

Matches John, Oohn, etc.

---

# NULL Values

NULL means value is missing or unknown.

Cannot use:

```sql
WHERE comment = NULL
```

Must use:

```sql
WHERE comment IS NULL
```

Example:

```sql
SELECT clientNo, viewDate
FROM Viewing
WHERE propertyNo='PG4'
AND comment IS NULL;
```

For non-null values:

```sql
WHERE comment IS NOT NULL
```

---

# ORDER BY

Sorts output.

Ascending (default):

```sql
SELECT *
FROM PropertyForRent
ORDER BY type;
```

Descending:

```sql
SELECT *
FROM Staff
ORDER BY salary DESC;
```

Multiple sorting keys:

```sql
SELECT *
FROM PropertyForRent
ORDER BY type, rent DESC;
```

Sort order:

1. type
2. rent (within each type)

---

# Aggregate Functions

Aggregate functions return a single value.

| Function | Purpose    |
| -------- | ---------- |
| COUNT()  | Count rows |
| SUM()    | Total      |
| AVG()    | Average    |
| MIN()    | Smallest   |
| MAX()    | Largest    |

---

### COUNT

Count rows:

```sql
SELECT COUNT(*)
FROM PropertyForRent;
```

Count unique values:

```sql
SELECT COUNT(DISTINCT propertyNo)
FROM Viewing;
```

---

### SUM

```sql
SELECT SUM(salary)
FROM Staff;
```

---

### AVG

```sql
SELECT AVG(salary)
FROM Staff;
```

---

### MIN and MAX

```sql
SELECT MIN(salary), MAX(salary)
FROM Staff;
```

---

### Multiple Aggregates

```sql
SELECT MIN(salary),
       MAX(salary),
       AVG(salary)
FROM Staff;
```

---

# GROUP BY

Used to create groups before applying aggregate functions.

Example:

Find number of staff and total salary in each branch.

```sql
SELECT branchNo,
       COUNT(staffNo) AS count,
       SUM(salary) AS sum
FROM Staff
GROUP BY branchNo;
```

Visual:

```text
Branch B001
  Staff 1
  Staff 2
  Staff 3
  ↓
COUNT = 3
SUM = total salary

Branch B002
  Staff 4
  Staff 5
  ↓
COUNT = 2
SUM = total salary
```

### Important Rule

Every non-aggregate column in SELECT must appear in GROUP BY.

Correct:

```sql
SELECT branchNo, COUNT(*)
FROM Staff
GROUP BY branchNo;
```

Wrong:

```sql
SELECT staffNo, COUNT(*)
FROM Staff;
```

---

# HAVING

Filters groups after GROUP BY.

Difference:

| WHERE        | HAVING         |
| ------------ | -------------- |
| Filters rows | Filters groups |

Example:

Find branches with more than 1 staff member.

```sql
SELECT branchNo,
       COUNT(*) AS count
FROM Staff
GROUP BY branchNo
HAVING COUNT(*) > 1;
```

Processing order:

```text
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
ORDER BY
```

---

# Subqueries

A query inside another query.

Structure:

```sql
SELECT ...
FROM ...
WHERE column =
      (SELECT ...);
```

---

### Example 1

Find staff working at branch located at 163 Main St.

```sql
SELECT staffNo, fName, lName
FROM Staff
WHERE branchNo =
(
    SELECT branchNo
    FROM Branch
    WHERE street='163 Main St'
);
```

---

### Example 2

Find staff earning above average salary.

```sql
SELECT staffNo, fName, lName
FROM Staff
WHERE salary >
(
    SELECT AVG(salary)
    FROM Staff
);
```

### Important Rules

* ORDER BY cannot be used inside a subquery.
* Subquery usually appears on the right side of comparison operators.
* Subquery must return one column unless EXISTS is used.

---

# Joins

Used when data comes from multiple tables.

### Why Join?

Suppose:

```text
Client Table
------------
clientNo
name

Viewing Table
-------------
clientNo
propertyNo
comment
```

Need information from both tables.

---

### Basic Join

```sql
SELECT c.clientNo,
       fName,
       lName,
       propertyNo,
       comment
FROM Client c, Viewing v
WHERE c.clientNo = v.clientNo;
```

Visual:

```text
Client
   |
clientNo
   |
Viewing
```

Rows are matched where clientNo is the same.

---

### Alternative Join Syntax

```sql
FROM Client c
JOIN Viewing v
ON c.clientNo = v.clientNo
```

---

# Multi-Table Join

Example:

```sql
SELECT b.branchNo,
       b.city,
       s.staffNo,
       propertyNo
FROM Branch b,
     Staff s,
     PropertyForRent p
WHERE b.branchNo = s.branchNo
AND s.staffNo = p.staffNo;
```

Visual:

```text
Branch
   |
branchNo
   |
 Staff
   |
staffNo
   |
PropertyForRent
```

---

# Join Processing (Exam Theory)

When SQL performs a join:

### Step 1

Create Cartesian Product

```text
Table A × Table B
```

Every row matched with every row.

---

### Step 2

Apply WHERE condition.

Keep matching rows only.

---

### Step 3

Select required columns.

---

### Step 4

Remove duplicates (if DISTINCT).

---

### Step 5

Sort (if ORDER BY exists).

---

# CROSS JOIN

Produces Cartesian Product.

```sql
SELECT *
FROM Table1
CROSS JOIN Table2;
```

Visual:

```text
3 rows × 4 rows
=
12 rows
```

---

# EXISTS

Returns TRUE if subquery returns at least one row.

Returns FALSE if subquery returns no rows.

Example:

Find staff working in a London branch.

```sql
SELECT staffNo, fName, lName
FROM Staff s
WHERE EXISTS
(
    SELECT *
    FROM Branch b
    WHERE s.branchNo = b.branchNo
    AND city='London'
);
```

Visual:

```text
Staff Row
    ↓
Check subquery
    ↓
Rows found?
    ↓
YES → include
NO  → exclude
```

---

# INSERT

Add new records.

### Insert all columns

```sql
INSERT INTO Staff
VALUES
('SG16','Alan','Brown',
 'Assistant','M',
 '1957-05-25',
 8300,'B003');
```

---

### Insert specific columns

```sql
INSERT INTO Staff
(staffNo,fName,lName,
 position,salary,branchNo)

VALUES
('SG44','Anne','Jones',
 'Assistant',8100,'B003');
```

---

# UPDATE

Modify existing records.

Syntax:

```sql
UPDATE tableName
SET column=value
WHERE condition;
```

### Example 1

Increase all salaries by 3%.

```sql
UPDATE Staff
SET salary = salary * 1.03;
```

---

### Example 2

Increase managers' salary by 5%.

```sql
UPDATE Staff
SET salary = salary * 1.05
WHERE position='Manager';
```

---

### Example 3

Promote employee.

```sql
UPDATE Staff
SET position='Manager',
    salary=18000
WHERE staffNo='SG14';
```

---

# DELETE

Remove records.

Syntax:

```sql
DELETE FROM tableName
WHERE condition;
```

---

### Example 1

Delete viewings for property PG4.

```sql
DELETE FROM Viewing
WHERE propertyNo='PG4';
```

---

### Example 2

Delete all rows.

```sql
DELETE FROM Viewing;
```

### Important

This deletes records only.

The table still exists.

---

# Most Important Exam Topics

### Filtering

```sql
WHERE
BETWEEN
IN
LIKE
IS NULL
```

### Sorting

```sql
ORDER BY
ASC
DESC
```

### Aggregate Functions

```sql
COUNT()
SUM()
AVG()
MIN()
MAX()
```

### Grouping

```sql
GROUP BY
HAVING
```

### Combining Tables

```sql
JOIN
EXISTS
Subquery
```

### Data Modification

```sql
INSERT
UPDATE
DELETE
```

### Easy Memory Flow

```text
SELECT → What to show
FROM → Where to get data
WHERE → Filter rows
GROUP BY → Create groups
HAVING → Filter groups
ORDER BY → Sort result
```

This flow is one of the most frequently tested SQL concepts in exams.

---
# Chap 4

Joins



A **join** is used when data needed in a query comes from more than one table.



The tables are connected through a common column (usually a primary key and foreign key).



---



### Basic Join (Inner Join)



Example: List names of all clients who viewed a property and any comment supplied.



```sql

SELECT c.clientNo, fName, lName,

       propertyNo, comment

FROM Client c, Viewing v

WHERE c.clientNo = v.clientNo;

```



### How it works



```text

Client Table                  Viewing Table



clientNo                      clientNo

C001                          C001

C002                          C003

C003                          C001

```



Join condition:



```sql

c.clientNo = v.clientNo

```



Only rows with matching client numbers are included.



```text

Client

   C001

     │

     │ matches

     │

Viewing

   C001

```



This is called an **Inner Join**.



Only matching rows are returned.



Also called an **Equi-Join** because the join condition uses "=".



---



### Alternative Inner Join Syntax



Instead of:



```sql

FROM Client c, Viewing v

WHERE c.clientNo = v.clientNo

```



You can write:



```sql

FROM Client c

JOIN Viewing v

ON c.clientNo = v.clientNo

```



Both produce the same result.



---



## Joining Two Tables



Example:



For each branch, list staff who manage properties and the properties they manage.



```sql

SELECT s.branchNo,

       s.staffNo,

       fName,

       lName,

       propertyNo

FROM Staff s, PropertyForRent p

WHERE s.staffNo = p.staffNo

ORDER BY s.branchNo, s.staffNo, propertyNo;

```



Relationship:



```text

Staff

------

staffNo



PropertyForRent

---------------

staffNo

```



Visual:



```text

Staff

  │

staffNo

  │

  ▼

PropertyForRent

```



The query matches staff members with the properties they manage.



---



## Joining Three Tables



Example:



For each branch, list staff who manage properties, including the city of the branch.



```sql

SELECT b.branchNo,

       b.city,

       s.staffNo,

       fName,

       lName,

       propertyNo

FROM Branch b,

     Staff s,

     PropertyForRent p

WHERE b.branchNo = s.branchNo

AND s.staffNo = p.staffNo

ORDER BY b.branchNo, s.staffNo, propertyNo;

```



Relationship:



```text

Branch

   │

branchNo

   │

Staff

   │

staffNo

   │

PropertyForRent

```



Visual:



```text

Branch

   │

   ▼

 Staff

   │

   ▼

PropertyForRent

```



The query combines information from all three tables.



---



### Alternative Join Syntax



Same query can be written as:



```sql

FROM (Branch b

      JOIN Staff s USING(branchNo))

      JOIN PropertyForRent p USING(staffNo)

```



You don't need to memorize this syntax unless your lecturer specifically focuses on it.



For exams, understanding the relationship is more important.



---



## Join + Aggregate Function



Example:



Find the number of properties handled by each staff member.



```sql

SELECT s.branchNo,

       s.staffNo,

       COUNT(*) AS myCount

FROM Staff s,

     PropertyForRent p

WHERE s.staffNo = p.staffNo

GROUP BY s.branchNo, s.staffNo

ORDER BY s.branchNo, s.staffNo;

```



Visual:



```text

Staff SG14

   ├── Property P1

   ├── Property P2

   └── Property P3



COUNT(*) = 3

```



Result:



| Staff | Properties Managed |

| ----- | ------------------ |

| SG14  | 3                  |

| SG37  | 2                  |

| SG5   | 4                  |



---



# How SQL Executes a Join



Exam theory question.



### Step 1: Create Cartesian Product



Every row from Table A is paired with every row from Table B.



Example:



Table A



| A |

| - |

| 1 |

| 2 |



Table B



| B |

| - |

| X |

| Y |



Cartesian Product:



| A | B |

| - | - |

| 1 | X |

| 1 | Y |

| 2 | X |

| 2 | Y |



Formula:



```text

Rows in A × Rows in B

```



Example:



```text

3 rows × 4 rows = 12 rows

```



---



### Step 2: Apply WHERE Condition



Example:



```sql

WHERE A.id = B.id

```



Only matching rows remain.



---



### Step 3: Select Columns



Apply SELECT clause.



```sql

SELECT name, salary

```



---



### Step 4: Remove Duplicates



Only if DISTINCT is used.



```sql

SELECT DISTINCT city

```



---



### Step 5: Sort Result



If ORDER BY exists.



```sql

ORDER BY salary DESC

```



---



# CROSS JOIN



Used when you want the complete Cartesian Product.



Syntax:



```sql

SELECT *

FROM Table1

CROSS JOIN Table2;

```



Visual:



```text

Table1

-------

A

B



Table2

-------

1

2



Result

-------

A 1

A 2

B 1

B 2

```



No matching condition is required.



---



# Outer Joins



### Problem with Inner Join



Inner join only returns matching rows.



If a row has no match, it is removed.



Example:



Branch table:



| Branch | City    |

| ------ | ------- |

| B1     | London  |

| B2     | Bristol |



Property table:



| Property | City   |

| -------- | ------ |

| P1       | London |



Inner Join:



```sql

SELECT *

FROM Branch b,

     Property p

WHERE b.city = p.city;

```



Result:



| Branch | Property |

| ------ | -------- |

| B1     | P1       |



Bristol branch disappears because no matching property exists.



---



## LEFT OUTER JOIN



Returns:



* All rows from the LEFT table

* Matching rows from the RIGHT table



If no match exists:



* Right side becomes NULL



Example:



```sql

SELECT b.*, p.*

FROM Branch1 b

LEFT JOIN PropertyForRent1 p

ON b.bCity = p.pCity;

```



Visual:



```text

LEFT TABLE = Branch



Branch

----------------

London

Bristol



Property

----------------

London



Result

----------------

London   Property

Bristol  NULL

```



Memory trick:



```text

LEFT JOIN

Keep everything on the LEFT

```



---



## RIGHT OUTER JOIN



Returns:



* All rows from the RIGHT table

* Matching rows from the LEFT table



If no match exists:



* Left side becomes NULL



Example:



```sql

SELECT b.*, p.*

FROM Branch1 b

RIGHT JOIN PropertyForRent1 p

ON b.bCity = p.pCity;

```



Visual:



```text

Branch

-------

London



Property

---------

London

Glasgow



Result

---------

London   Property

NULL     Glasgow Property

```



Memory trick:



```text

RIGHT JOIN

Keep everything on the RIGHT

```



---



## FULL OUTER JOIN



Returns:



* Matching rows

* Unmatched rows from left table

* Unmatched rows from right table



Example:



```sql

SELECT b.*, p.*

FROM Branch1 b

FULL JOIN PropertyForRent1 p

ON b.bCity = p.pCity;

```



Visual:



```text

Branch

---------

London

Bristol



Property

---------

London

Glasgow



Result

--------------------

London    Property

Bristol   NULL

NULL      Glasgow

```



Memory trick:



```text

FULL JOIN

Keep EVERYTHING

```



---



## Join Types Comparison



### INNER JOIN



```text

Branch  ←match→ Property

```



Only matching rows.



---



### LEFT JOIN



```text

ALL Branches

+

Matching Properties

```



Unmatched property columns = NULL



---



### RIGHT JOIN



```text

ALL Properties

+

Matching Branches

```



Unmatched branch columns = NULL



---



### FULL JOIN



```text

ALL Branches

+

ALL Properties

```



Unmatched values become NULL.



---



### Exam Memory Table



| Join Type  | Returns                             |

| ---------- | ----------------------------------- |

| INNER JOIN | Matching rows only                  |

| LEFT JOIN  | All left rows + matching right rows |

| RIGHT JOIN | All right rows + matching left rows |

| FULL JOIN  | All rows from both tables           |

| CROSS JOIN | Cartesian product                   |



### Easy Visual Memory



```text

INNER JOIN

    A ∩ B



LEFT JOIN

    A + (A ∩ B)



RIGHT JOIN

    B + (A ∩ B)



FULL JOIN

    A + B



CROSS JOIN

    A × B

```



For SQL exams, the most commonly tested join concepts are:



1. Inner Join

2. Left Join

3. Group By with Join

4. Difference between Inner Join and Outer Join

5. Cartesian Product / Cross Join

6. Steps SQL uses to process a join query.
---

# Chap 5
Stored Procedures

A **Stored Procedure** is a collection of SQL statements stored in the database and executed as a single unit.

Think of it as a **saved SQL program** that can be run whenever needed.

---

## Why Use Stored Procedures?

### 1. Perform Operations

Can contain multiple SQL statements.

Example:

```sql
SELECT ...
INSERT ...
UPDATE ...
DELETE ...
```

All can be grouped into one procedure.

---

### 2. Accept Input Parameters

Allows users to pass values into the procedure.

Example:

```sql
EXEC ProductList 4
```

Here, `4` is the input parameter.

---

### 3. Return Values

Can return:

* Success status
* Failure status
* Output values

---

### 4. Share Application Logic

All users execute the same procedure.

Benefits:

* Consistent results
* No duplicated SQL code

---

### 5. Hide Database Structure

Users execute procedures without accessing tables directly.

Instead of:

```sql
SELECT *
FROM Product
```

Users run:

```sql
EXEC ProductList
```

The table structure remains hidden.

---

### 6. Improve Security

Users can be given permission to execute a procedure even if they cannot access the underlying tables.

```text
User
  ↓
Stored Procedure
  ↓
Table
```

User never touches the table directly.

---

### 7. Improve Performance

Stored procedures are compiled into an execution plan.

```text
SQL Statements
       ↓
Execution Plan
       ↓
Stored Procedure
```

The database can reuse the plan, making execution faster.

---

### 8. Reduce Network Traffic

Without Stored Procedure:

```text
Client → SQL Statement 1
Client → SQL Statement 2
Client → SQL Statement 3
Client → SQL Statement 4
```

With Stored Procedure:

```text
Client → EXEC ProcedureName
```

Only one request is sent.

---

# Creating a Stored Procedure

Syntax:

```sql
CREATE PROCEDURE ProcedureName
AS
    SQL Statements
```

Example:

```sql
CREATE PROCEDURE Production.LongLeadProducts
AS
SELECT Name, ProductNumber
FROM Production.Product
WHERE DaysToManufacture >= 1
```

Execute:

```sql
EXECUTE Production.LongLeadProducts
```

or

```sql
EXEC Production.LongLeadProducts
```

---

## Visual

```text
Stored Procedure: LongLeadProducts

          EXEC
            ↓
    LongLeadProducts
            ↓
      SELECT Query
            ↓
         Results
```

---

# Good Practices

### Qualify Object Names

Use:

```sql
Production.Product
```

instead of:

```sql
Product
```

This avoids ambiguity.

---

### One Procedure = One Task

Good:

```text
GetProductList
AddDepartment
DeleteEmployee
```

Bad:

```text
DoEverything
```

Keep procedures focused on a single task.

---

### Create → Test → Troubleshoot

Process:

```text
Create
   ↓
Test
   ↓
Fix Errors
   ↓
Deploy
```

---

### Avoid "sp_" Prefix

Avoid:

```sql
sp_GetProducts
```

Use:

```sql
GetProducts
```

Reason:

* SQL Server reserves many system procedures beginning with `sp_`.
* May reduce performance.

---

# ALTER PROCEDURE

Used to modify an existing procedure.

Syntax:

```sql
ALTER PROCEDURE ProcedureName
AS
    SQL Statements
```

Example:

```sql
ALTER PROC Production.LongLeadProducts
AS
SELECT Name,
       ProductNumber,
       DaysToManufacture
FROM Production.Product
WHERE DaysToManufacture >= 1
ORDER BY DaysToManufacture DESC, Name
```

---

## Visual

```text
Existing Procedure
         ↓
     ALTER
         ↓
Updated Procedure
```

---

# DROP PROCEDURE

Used to remove a procedure.

Syntax:

```sql
DROP PROCEDURE ProcedureName
```

Example:

```sql
DROP PROC Production.LongLeadProducts
```

---

## Visual

```text
Procedure Exists
       ↓
DROP
       ↓
Procedure Deleted
```

---

# Parameters

Parameterized procedures can contain:

1. Input Parameters
2. Output Parameters
3. Return Values

---

# Input Parameters

Input parameters allow values to be passed into a procedure.

Example:

```sql
ALTER PROC Production.LongLeadProducts
    @MinimumLength INT = 1
AS

SELECT Name,
       ProductNumber,
       DaysToManufacture
FROM Production.Product
WHERE DaysToManufacture >= @MinimumLength
```

Run:

```sql
EXEC Production.LongLeadProducts
     @MinimumLength = 4
```

---

## Visual

```text
User Input
    4
    ↓
@MinimumLength
    ↓
Procedure
    ↓
Results
```

---

# Default Values

Input parameters can have default values.

Example:

```sql
@MinimumLength INT = 1
```

If user does not supply a value:

```sql
EXEC Production.LongLeadProducts
```

Then:

```text
@MinimumLength = 1
```

automatically.

---

# Parameter Validation

Always validate input values.

Example:

```sql
IF (@MinimumLength < 0)
BEGIN
    RAISERROR('Invalid lead time.',14,1)
    RETURN
END
```

Purpose:

* Prevent invalid data.
* Improve reliability.

---

## Visual

```text
Input
  ↓
Validation
  ↓
Valid? ── No → Error
  │
 Yes
  ↓
Execute Query
```

---

# Output Parameters

Output parameters return data back to the caller.

Example:

```sql
CREATE PROC AddDepartment
    @Name NVARCHAR(50),
    @GroupName NVARCHAR(50),
    @DeptID SMALLINT OUTPUT
```

Output parameter:

```sql
@DeptID OUTPUT
```

After insertion:

```sql
SET @DeptID = SCOPE_IDENTITY()
```

The new department ID is returned.

---

## Visual

```text
Input Values
      ↓
Stored Procedure
      ↓
Insert Record
      ↓
Generate DeptID
      ↓
Return DeptID
```

---

# Return Values

A procedure can return a status code.

Common convention:

| Return Value | Meaning |
| ------------ | ------- |
| 0            | Success |
| -1           | Failure |

Example:

```sql
IF ((@Name='') OR (@GroupName=''))
    RETURN -1
```

Success:

```sql
RETURN 0
```

---

## Visual

```text
Procedure
   ↓
Success? ── No → -1
   │
  Yes
   ↓
   0
```

---

# Complete Example

### Procedure

```sql
CREATE PROC HumanResources.AddDepartment
    @Name NVARCHAR(50),
    @GroupName NVARCHAR(50),
    @DeptID SMALLINT OUTPUT
AS

IF ((@Name='') OR (@GroupName=''))
    RETURN -1

INSERT INTO HumanResources.Department
(Name, GroupName)
VALUES (@Name, @GroupName)

SET @DeptID = SCOPE_IDENTITY()

RETURN 0
```

---

### Execute Procedure

```sql
DECLARE @dept INT,
        @result INT

EXEC @result =
AddDepartment
    'Refunds',
    '',
    @dept OUTPUT
```

---

### Check Result

```sql
IF (@result = 0)
    SELECT @dept
ELSE
    SELECT 'Error during insert'
```

---

## Flow of Example

```text
Call Procedure
       ↓
Validate Inputs
       ↓
Valid?
 ┌─────────────┐
 │ No          │
 ↓             │
RETURN -1      │
               │
 │ Yes         │
 ↓             │
Insert Record  │
 ↓             │
Generate ID    │
 ↓             │
OUTPUT DeptID  │
 ↓             │
RETURN 0       │
 └─────────────┘
```

---

## Exam Points to Remember

### Stored Procedure

* Saved collection of SQL statements.
* Executed as one unit.

### Commands

```sql
CREATE PROCEDURE
ALTER PROCEDURE
DROP PROCEDURE
EXECUTE (EXEC)
```

### Parameter Types

| Type             | Purpose                     |
| ---------------- | --------------------------- |
| Input Parameter  | Pass data into procedure    |
| Output Parameter | Return data to caller       |
| Return Value     | Return success/failure code |

### Benefits

* Reuse SQL code.
* Better security.
* Faster execution.
* Reduced network traffic.
* Hides database structure.

### Common Exam Question

Difference between Output Parameter and Return Value:

| Output Parameter               | Return Value          |
| ------------------------------ | --------------------- |
| Returns actual data            | Returns status code   |
| Can return IDs, totals, values | Usually 0 or -1       |
| Declared with OUTPUT           | Uses RETURN statement |

### Easy Memory

```text
CREATE  → Create procedure
EXEC    → Run procedure
ALTER   → Modify procedure
DROP    → Delete procedure

Input Parameter  → Data goes IN
Output Parameter → Data comes OUT
Return Value     → Success / Failure
```
---
# Chap 6
Integrity Constraints and Triggers

## Integrity Constraints

Integrity constraints are rules that ensure data in a database is accurate and consistent.

There are **5 types of integrity constraints**:

1. Required Data
2. Domain Constraints
3. Entity Integrity
4. Referential Integrity
5. Enterprise Constraints (Business Rules)

---

## 1. Required Data

Some columns must always contain a value.

Example:

Every staff member must have a job position.

```sql
ALTER TABLE Staff
ALTER COLUMN position VARCHAR(50) NOT NULL;
```

### Meaning

```text
Staff
--------------------
staffNo   position
S001      Manager   ✓
S002      NULL      ✗
```

`NOT NULL` prevents empty values.

---

## 2. Domain Constraints

A domain defines the valid values that can be stored in a column.

Example:

Gender can only be:

```text
M
F
```

Constraint:

```sql
ALTER TABLE Staff WITH NOCHECK
ADD CONSTRAINT CK1
CHECK (gender='M' OR gender='F');
```

### Visual

```text
gender

M ✓
F ✓
A ✗
Male ✗
NULL ? (depends on NOT NULL)
```

### Common Constraints

```sql
CHECK(age > 0)

CHECK(salary >= 0)

CHECK(gender IN ('M','F'))
```

---

## 3. Entity Integrity

Every table must have a primary key.

A Primary Key:

* Must be unique.
* Cannot be NULL.

Example:

```sql
PRIMARY KEY(staffNo)
```

Composite Primary Key:

```sql
PRIMARY KEY(clientNo, propertyNo)
```

### Visual

```text
Staff

staffNo
-------
S001 ✓
S002 ✓
S001 ✗ Duplicate
NULL ✗
```

### Alternate Keys

If another column must also be unique:

```sql
UNIQUE(telNo)
```

Example:

```text
telNo

0123456789 ✓
0123456789 ✗
```

---

## 4. Referential Integrity

Maintains relationships between tables.

### Foreign Key

A Foreign Key (FK) references a Primary Key (PK) in another table.

Example:

```sql
FOREIGN KEY(branchNo)
REFERENCES Branch(branchNo)
```

### Visual

```text
Branch (Parent)

branchNo
--------
B001
B002

Staff (Child)

staffNo   branchNo
------------------
S001      B001 ✓
S002      B002 ✓
S003      B999 ✗
```

Foreign key values must exist in the parent table.

---

## Referential Actions

When a parent row is updated or deleted, SQL needs to know what to do with child rows.

### CASCADE

Delete parent → delete matching child rows.

```sql
ON DELETE CASCADE
```

Visual:

```text
Branch B001
     ↓
Staff S001
Staff S002

Delete B001
     ↓
Delete S001
Delete S002
```

---

### SET NULL

Delete parent → set FK to NULL.

```sql
ON DELETE SET NULL
```

Visual:

```text
Before

S001  B001

Delete B001

After

S001  NULL
```

---

### SET DEFAULT

Delete parent → FK becomes default value.

```sql
ON DELETE SET DEFAULT
```

Example:

```text
Default Branch = B000
```

---

### NO ACTION

Reject deletion.

```sql
ON DELETE NO ACTION
```

Default behavior.

Visual:

```text
Cannot delete parent
because child rows still exist.
```

---

### Examples

```sql
FOREIGN KEY(staffNo)
REFERENCES Staff
ON DELETE SET NULL
```

```sql
FOREIGN KEY(ownerNo)
REFERENCES Owner
ON UPDATE CASCADE
```

---

## 5. Enterprise Constraints (Business Rules)

Rules specific to an organization.

Examples:

### Rule 1

A staff member cannot manage more than 100 properties.

```text
Staff
  ↓
Maximum 100 properties
```

### Rule 2

Managers cannot earn more than 30000.

```text
Position = Manager
Salary <= 30000
```

These rules are usually too complex for normal CHECK constraints.

They are often enforced using **Triggers**.

---

# Triggers

A trigger is a special type of stored procedure that runs automatically when a specific event occurs.

Unlike stored procedures:

```text
Stored Procedure
      ↓
Must be called manually
```

```text
Trigger
      ↓
Runs automatically
```

---

## Uses of Triggers

Triggers can:

* Enforce business rules.
* Maintain data integrity.
* Record audit information.
* Prevent invalid operations.
* Update related tables automatically.
* Roll back transactions.

---

# Trigger Categories

### 1. DML Triggers

Respond to:

```text
INSERT
UPDATE
DELETE
```

Most important for exams.

---

### 2. DDL Triggers

Respond to:

```text
CREATE TABLE
ALTER TABLE
DROP TABLE
```

---

### 3. Logon Triggers

Respond when users log in.

---

# DML Trigger Events

## INSERT Trigger

Runs when data is inserted.

Example:

```text
New Order Added
      ↓
Update Inventory
```

Visual:

```text
INSERT
   ↓
Trigger Fires
   ↓
Additional Action
```

---

## UPDATE Trigger

Runs when data is modified.

Example:

```text
Salary Changed
      ↓
Log Change
```

---

## DELETE Trigger

Runs when data is deleted.

Example:

```text
Customer Deleted
      ↓
Mark Customer Inactive
```

Instead of removing data completely.

---

# AFTER vs INSTEAD OF Triggers

## AFTER Trigger

The original action happens first.

```text
INSERT
   ↓
Data Saved
   ↓
Trigger Runs
```

Example:

```sql
AFTER INSERT
```

---

## INSTEAD OF Trigger

The original action never happens.

```text
DELETE Requested
       ↓
Delete Blocked
       ↓
Trigger Runs Instead
```

Example:

```sql
INSTEAD OF DELETE
```

Commonly used on views.

---

# Inserted and Deleted Tables

Triggers use two special temporary tables:

| Table    | Contains |
| -------- | -------- |
| inserted | New rows |
| deleted  | Old rows |

---

## INSERT Operation

```text
INSERT row
     ↓
inserted table
```

Example:

```text
New Employee

stored in inserted
```

---

## DELETE Operation

```text
DELETE row
     ↓
deleted table
```

Example:

```text
Deleted Employee

stored in deleted
```

---

## UPDATE Operation

SQL treats UPDATE as:

```text
DELETE old row
      +
INSERT new row
```

Visual:

```text
Before Update
      ↓
deleted table

After Update
      ↓
inserted table
```

### Memory Trick

```text
INSERT
  inserted only

DELETE
  deleted only

UPDATE
  both inserted and deleted
```

---

# Creating a Trigger

Syntax:

```sql
CREATE TRIGGER trigger_name
ON table_name
AFTER INSERT
AS
BEGIN
    SQL statements
END
```

General form:

```sql
CREATE TRIGGER trigger_name
ON table_name
AFTER INSERT, UPDATE, DELETE
AS
BEGIN
   SQL statements
END
```

---

# AFTER INSERT Trigger Example

When a WorkOrder is inserted, create a TransactionHistory record.

```text
WorkOrder Added
      ↓
Trigger Fires
      ↓
TransactionHistory Updated
```

Flow:

```text
INSERT WorkOrder
       ↓
inserted table
       ↓
AFTER INSERT Trigger
       ↓
Insert TransactionHistory
```

---

# Business Rule Trigger Example

Vendor credit rating must not be 5.

```text
New Purchase Order
         ↓
Check Vendor Rating
         ↓
Rating = 5 ?
```

If YES:

```sql
RAISERROR(...)
ROLLBACK TRANSACTION
```

Visual:

```text
Insert Order
      ↓
Check Credit Rating
      ↓
Too Low?
      ↓
YES → Cancel Transaction
NO  → Continue
```

---

# AFTER DELETE Trigger

Example:

When a category is deleted:

Instead of deleting products, mark them discontinued.

```text
Delete Category
      ↓
Trigger Fires
      ↓
Products Updated
```

Visual:

```text
Category Deleted
       ↓
deleted table
       ↓
UPDATE Products
SET Discontinued = 1
```

---

# AFTER UPDATE Trigger

Used when data changes.

Example:

Automatically update ModifiedDate.

```text
Product Review Updated
         ↓
Trigger Fires
         ↓
ModifiedDate Updated
```

Visual:

```text
Old Data
   ↓
deleted table

New Data
   ↓
inserted table

Trigger compares changes
```

---

## IF UPDATE

Checks whether a specific column was updated.

Example:

```sql
IF UPDATE(Salary)
```

Meaning:

```text
Did Salary change?
```

If yes:

```text
Run Trigger Logic
```

---

# INSTEAD OF Trigger

Runs instead of the requested action.

Example:

```sql
INSTEAD OF DELETE
```

Visual:

```text
DELETE Employee
        ↓
Delete Prevented
        ↓
Trigger Executes
```

Useful when:

* Preventing deletion.
* Validating operations.
* Updating views.

---

# Why Use Triggers Instead of CHECK Constraints?

CHECK constraints can only validate columns in the same table.

Example:

```sql
CHECK (salary > 0)
```

Works.

But:

```text
Manager cannot manage more than 100 properties
```

Requires checking another table.

CHECK cannot do this.

Trigger can.

---

# Common Trigger Uses

### Business Rules

```text
Manager salary ≤ 30000
```

### Auditing

```text
Who changed salary?
When?
```

### Automatic Updates

```text
Order Created
      ↓
Inventory Updated
```

### Validation

```text
Credit Rating Check
```

### Prevent Deletion

```text
Customer cannot be deleted
```

---

# Alter and Drop Trigger

## Modify Trigger

```sql
ALTER TRIGGER trigger_name
ON table_name
AFTER INSERT
AS
...
```

---

## Delete Trigger

```sql
DROP TRIGGER trigger_name
```

---

# Exam Focus

### Integrity Constraints

| Type                  | Purpose        |
| --------------------- | -------------- |
| Required Data         | NOT NULL       |
| Domain Constraint     | CHECK          |
| Entity Integrity      | PRIMARY KEY    |
| Referential Integrity | FOREIGN KEY    |
| Enterprise Constraint | Business Rules |

---

### Referential Actions

| Action      | Result                   |
| ----------- | ------------------------ |
| CASCADE     | Delete/update child rows |
| SET NULL    | FK becomes NULL          |
| SET DEFAULT | FK becomes default value |
| NO ACTION   | Reject operation         |

---

### Trigger Types

| Trigger      | When Fires               |
| ------------ | ------------------------ |
| AFTER INSERT | After insert             |
| AFTER UPDATE | After update             |
| AFTER DELETE | After delete             |
| INSTEAD OF   | Replaces original action |

---

### Special Tables

| Operation | inserted | deleted |
| --------- | -------- | ------- |
| INSERT    | ✓        | ✗       |
| DELETE    | ✗        | ✓       |
| UPDATE    | ✓        | ✓       |

### Easy Memory

```text
NOT NULL      → Required Data
CHECK         → Domain Constraint
PRIMARY KEY   → Entity Integrity
FOREIGN KEY   → Referential Integrity
TRIGGER       → Business Rules

INSERT  → inserted table
DELETE  → deleted table
UPDATE  → both tables

AFTER      → Action first, trigger later
INSTEAD OF → Trigger first, action blocked
```
---
# Chap 7
Database Administration (DA & DBA)

## Introduction

A **DBMS (Database Management System)** is only a tool.

Having a good DBMS **does not automatically create a good information system**.

To be successful, the database must be properly planned, managed, and supported.

The introduction of a DBMS can have:

### Positive Effects

* Better data sharing
* Better security
* Reduced duplication
* Improved decision making

### Negative Effects

* Resistance from employees
* Higher costs
* Need for training
* More management responsibilities

---

## Three Important Aspects of Database Administration

| Aspect        | Description                                  |
| ------------- | -------------------------------------------- |
| Technological | DBMS software and hardware                   |
| Managerial    | Administration and management functions      |
| Cultural      | Employee acceptance and resistance to change |

### Visual

```text
Database Administration

        ┌─────────────┐
        │ Technology  │
        └──────┬──────┘
               │
        ┌──────┴──────┐
        │ Management  │
        └──────┬──────┘
               │
        ┌──────┴──────┐
        │  Culture    │
        └─────────────┘
```

---

## Why Database Administration is Important

Tasks include:

* Selecting DBMS
* Installing DBMS
* Configuring DBMS
* Monitoring DBMS
* Managing storage
* Managing security
* Supporting users

People involved:

* Programmers
* Managers
* End users

---

## Requirements for Successful Database Administration

### Technical Skills

Knowledge of:

* DBMS
* Hardware
* Security
* Networking
* Backup and recovery

### Managerial Skills

Ability to:

* Plan
* Organize
* Coordinate
* Manage staff

### Communication Skills

Need to:

* Work with users
* Gather requirements
* Solve conflicts
* Explain benefits of database systems

---

## Organizational Impact of DBMS

When a DBMS is introduced:

### Changes in People

* New employees may be hired
* New roles created
* Performance may be monitored differently

### Changes in Departments

Departments may need to share data.

Example:

```text
Before

Sales Department
      Own Data

HR Department
      Own Data
```

```text
After

Shared Database
      ↑
Sales
HR
Finance
Marketing
```

Managers lose exclusive ownership of data.

---

## Evolution of Database Administration

### Stage 1: Departmental Data Processing

Each department stores its own files.

```text
Sales Files

HR Files

Finance Files
```

Problems:

* Duplicate data
* Inconsistency
* Difficult sharing

---

### Stage 2: Centralized Electronic Data Processing

Data processing becomes more centralized.

```text
Departments
      ↓
Central Computer
```

---

### Stage 3: Information Systems Department

Formal department created to manage information.

```text
Users
  ↓
Information Systems Department
```

---

### Stage 4: Database Administration

Shared databases create the need for dedicated database management.

```text
Shared Database
       ↓
DA + DBA
```

---

# Data Administrator (DA)

### Definition

A **Data Administrator (DA)** is responsible for the overall management of organizational data resources.

Focuses on:

* Corporate-wide data management
* Policies
* Standards
* Planning

### Characteristics

| Feature     | DA                |
| ----------- | ----------------- |
| Level       | High              |
| Focus       | Managerial        |
| Scope       | Organization-wide |
| Orientation | Strategic         |

---

## Responsibilities of DA

### Set Data Goals

Determine how data should support business objectives.

---

### Create Data Policies

Policies are general rules.

Example:

```text
Customer information must be protected.
```

---

### Create Standards

Standards are detailed requirements.

Example:

```text
All customer IDs must contain 8 digits.
```

---

### Long-Term Planning

Plans future database requirements.

Example:

```text
Need cloud database in next 5 years.
```

---

### Conceptual and Logical Database Design

Involved in:

```text
Requirements
      ↓
Conceptual Design
      ↓
Logical Design
```

---

### Security Planning

Works with DBA to develop security strategies.

---

### Data Management Scope

DA manages:

```text
Computerized Data
Manual Data
External Data
```

Not only DBMS data.

---

## Visual Summary of DA

```text
Data Administrator (DA)

     Policies
         │
     Standards
         │
     Planning
         │
     Security
         │
 Conceptual Design
```

---

# Database Administrator (DBA)

### Definition

A **Database Administrator (DBA)** is responsible for technical database management.

Focuses on:

* Database operation
* Security
* Performance
* Backup and recovery

### Characteristics

| Feature     | DBA           |
| ----------- | ------------- |
| Level       | Lower         |
| Focus       | Technical     |
| Scope       | DBMS-specific |
| Orientation | Operational   |

---

## Responsibilities of DBA

### Physical Database Design

Responsible for:

```text
Tables
Indexes
Storage
Files
```

---

### Database Control

Controls:

* Database access
* Database operation
* Database maintenance

---

### Centralized and Distributed Databases

#### Centralized Database

```text
One Database
      ↓
One DBA
```

#### Distributed Database

```text
Location A
Location B
Location C
      ↓
System DBA
```

More coordination is required.

---

# Main DBA Responsibilities

## 1. Selection of DBMS, Utilities and Hardware

Important factors:

* DBMS model
* Storage capacity
* Security
* Backup and recovery
* Concurrency control
* Performance
* Cost
* Vendor support

### Visual

```text
Choose DBMS

Security
Storage
Performance
Cost
Support
```

---

## 2. End User Support

Responsibilities:

* Gather requirements
* Solve user problems
* Provide training
* Improve user confidence

### Example

```text
User Problem
      ↓
DBA Support
      ↓
Solution
```

---

## 3. Enforcing Policies, Procedures and Standards

### Policy

General direction.

Example:

```text
Protect customer data.
```

### Standard

Specific requirement.

Example:

```text
Passwords must be 8 characters.
```

### Procedure

Step-by-step instructions.

Example:

```text
Backup process:
1. Stop system
2. Run backup
3. Verify backup
```

---

## 4. Data Security, Privacy and Integrity

One of the most important DBA responsibilities.

### Challenges

Especially difficult in distributed systems.

Need to protect against:

* Unauthorized access
* Data corruption
* External attacks

---

### Security Measures

```text
Firewalls
Proxy Servers
Passwords
Access Privileges
Encryption
```

---

## 5. Backup and Recovery

DBA must ensure data can be recovered after failure.

### Requirements

#### Regular Backups

```text
Daily
Weekly
Monthly
```

#### Backup Identification

Clearly label backups.

```text
Backup_2026_06_14
```

#### Multiple Copies

Store backups at different locations.

```text
Main Site
Backup Site
Cloud Storage
```

---

### Physical Protection

Protect:

* Hardware
* Software
* Backup media

Methods:

```text
Restricted Access
Fire Protection
Air Conditioning
```

---

## 6. Data Distribution and Use

Data must reach:

* Right user
* Right time
* Right format

Modern methods:

```text
Web Applications
Query Tools
Internet Access
```

Benefits:

* Faster access
* Less dependence on programmers

---

## 7. Database Design and Implementation

DBA provides:

### Data Modeling

```text
ERD Design
Logical Design
```

### Database Implementation

```text
Create Tables
Create Relationships
Create Constraints
```

### Operational Procedures

```text
Backup Plans
Recovery Plans
Security Plans
```

---

## 8. Authorization Management

Controls user access.

### User Access Management

#### Define Users

```text
Ali
John
Mary
```

#### Assign Passwords

```text
User → Password
```

#### Create User Groups

```text
Managers
Staff
Admins
```

#### Assign Privileges

```text
Read
Insert
Update
Delete
```

---

### View Definition

Limit what users can see.

Example:

```text
HR can see salaries

Sales cannot see salaries
```

Using:

```sql
VIEW
```

---

### DBMS Utility Access Control

Control use of:

```text
Query Tools
Report Tools
Administration Tools
```

---

### Usage Monitoring

Track user activity.

Example:

```text
Who accessed data?
When?
What changes were made?
```

Create:

```text
Audit Log
```

---

# DA vs DBA (Very Important Exam Table)

| Area           | Data Administrator (DA)  | Database Administrator (DBA) |
| -------------- | ------------------------ | ---------------------------- |
| Level          | High level               | Low level                    |
| Focus          | Managerial               | Technical                    |
| Scope          | Organization-wide        | DBMS-specific                |
| Planning       | Long-term                | Short-term                   |
| Design         | Conceptual & Logical     | Physical                     |
| Policies       | Creates                  | Enforces                     |
| Security       | Strategic planning       | Technical implementation     |
| Responsibility | Corporate data resources | Database operation           |

---

## Easy Memory

```text
DA = Decide

Policies
Standards
Planning
Organization-wide
```

```text
DBA = Do

Security
Backup
Recovery
Performance
Users
Database Operation
```

---

# Exam Focus

### DA

* High-level role
* Corporate-wide data management
* Policies, standards, planning
* Conceptual & logical design

### DBA

* Technical role
* Physical database design
* Security
* Backup & recovery
* User access management
* Performance tuning

### Difference

```text
DA = Manager

DBA = Technician
```
### Contrasting DA and DBA Activities and Characteristics
| DA | DBA |
|----|-----|
| Strategic planning | Control and supervision |
| Sets long-term goals | Executes plans to reach goals |
| Sets policies and standards | Enforces policies and procedures; enforces programming standards |
| Broad scope | Narrow scope |
| Long-term focus | Short-term focus on daily operations |
| Managerial orientation | Technical orientation |
| DBMS independent | DBMS specific |

### Remember

```text
DA decides WHAT should be done.

DBA decides HOW to do it.
```

---
# Chap 8
# Database Security

## Scope of Database Security

Database security covers everything needed to protect a database system from misuse, damage, or unauthorized access.

It includes protection of:

* Data stored in the database
* DBMS software
* Hardware and servers
* Network connections
* Users and access points
* Backup and recovery systems

### Key idea

Security is not only about the database itself, but the **entire system environment**.

---

## Why Database Security is a Serious Concern

A database is one of the most valuable assets in an organization.

It is important because:

* Data has **business and strategic value**
* Data is often **confidential and sensitive**
* Many users access the same database
* Systems are connected to networks and the internet

### Risks if security fails:

* Financial loss
* Legal problems
* Reputation damage
* Business disruption

---

## Types of Threats to a Database System

Database systems face many threats:

### 1. Theft and Fraud

* Stealing data (e.g. customer records, credit cards)
* Manipulating data for personal gain

---

### 2. Loss of Confidentiality

* Unauthorized users viewing private data
* Example: salary information leaked

---

### 3. Loss of Privacy

* Personal information exposed without permission

---

### 4. Loss of Integrity

* Data is changed incorrectly or maliciously
* Example: changing account balances

---

### 5. Loss of Availability

* Users cannot access the database
* Caused by:

  * System crashes
  * Attacks (e.g. denial of service)
  * Hardware failure

---

## Key Security Concepts

### Authentication

Checks **who the user is**.

Example:

* Username + password
* Fingerprint / biometrics

```text id="auth1"
User → Login → System verifies identity
```

---

### Authorization

Defines **what the user is allowed to do**.

Example:

* Read data
* Insert data
* Update data
* Delete data

```text id="auth2"
User is valid → System checks permissions → Access granted or denied
```

---

## Main Issues in Database Security

### 1. Legal and Ethical Issues

* Who is allowed to access data?
* What data can be viewed or used?

---

### 2. Policy Issues

* Who enforces security?

  * Government
  * Organization
  * Department

---

### 3. System-Level Issues

* Where should security be enforced?
* How should it be implemented?

---

## Access Control

Access control decides:

* Who can access the database
* What data they can access
* What operations they can perform

Usually enforced using:

* User accounts
* Passwords
* Privileges

---

## Components of Authorization

Authorization is based on 3 main concepts:

### 1. Users

Individuals who access the database.

Example:

* Smith
* Jones
* DBA

---

### 2. Objects

Database items being protected.

Examples:

* Tables
* Columns
* Rows

---

### 3. Privileges

Actions allowed on objects.

Examples:

* SELECT (read)
* INSERT (add)
* UPDATE (modify)
* DELETE (remove)

---

## Types of Security

### 1. User-Based Security

* Security assigned to each user
* Each user gets specific permissions

Example:

* Smith can insert data
* Jones can only read data

---

### 2. Object-Based Security

* Security assigned to objects
* Each table defines who can access it

Example:

* Employees table → only HR can access

---

## SQL Security Commands

## GRANT (Give Permission)

Used to give access rights.

### Syntax:

```sql id="grant1"
GRANT action
ON object
TO user;
```

---

### Example:

```sql id="grant2"
GRANT SELECT, INSERT, UPDATE, DELETE
ON employees, departments
TO Smith;
```

---

### Grant with GRANT OPTION

Allows user to pass permissions to others.

```text id="grant3"
DBA → Smith → Jones
```

Example:

```sql id="grant4"
GRANT SELECT
ON employees
TO DBA
WITH GRANT OPTION;
```

---

### Column-Level Permission

You can restrict access to specific columns.

Example:

```sql id="grant5"
GRANT UPDATE(price)
ON products
TO Jones;
```

---

### Default Rule

If no GRANT is given:

```text id="grant6"
User has NO access
```

---

## REVOKE (Remove Permission)

Used to remove access rights.

### Syntax:

```sql id="revoke1"
REVOKE action
ON object
FROM user;
```

---

### Example:

```sql id="revoke2"
REVOKE INSERT, UPDATE, DELETE, SELECT
ON employees
FROM Smith;
```

---

### Remove All Permissions

```sql id="revoke3"
REVOKE ALL PRIVILEGES
ON employees
FROM Smith;
```

---

## Visual Summary

### GRANT Flow

```text id="flow1"
DBA
 ↓
GRANT permissions
 ↓
User gains access
```

---

### REVOKE Flow

```text id="flow2"
DBA
 ↓
REVOKE permissions
 ↓
User loses access
```

---

## Key Exam Points

### Database Security Includes:

* Data protection
* System protection
* User access control
* Network protection

---

### Types of Threats:

* Theft and fraud
* Confidentiality loss
* Privacy loss
* Integrity loss
* Availability loss

---

### Security Concepts:

| Term           | Meaning              |
| -------------- | -------------------- |
| Authentication | Who the user is      |
| Authorization  | What the user can do |

---

### SQL Security:

| Command | Purpose            |
| ------- | ------------------ |
| GRANT   | Give permissions   |
| REVOKE  | Remove permissions |

---

### Important Idea:

```text id="key1"
Authentication → Identity check
Authorization → Permission check
```

---

### Simple Memory Aid:

```text id="key2"
GRANT = Give access
REVOKE = Remove access

Authentication = "Who are you?"
Authorization = "What can you do?"
```
---
# Chap 9
Transactions, Concurrency Control, and Recovery

## Transaction

A **transaction** is a sequence of database operations (read/write) treated as a single unit of work.

It is used to:

* read data
* update data
* maintain consistency

### Key idea

A transaction moves the database from one **consistent state → another consistent state**

Even if temporary inconsistency happens during execution.

---

## Transaction Outcomes

A transaction has two possible results:

### 1. Commit (Success)

* Transaction completes successfully
* Changes become permanent
* Database reaches a new consistent state

### 2. Abort / Rollback (Failure)

* Transaction fails
* All changes are undone
* Database returns to original state

```text id="tx1"
Start → Work → Commit → Permanent changes
Start → Work → Fail → Rollback (undo)
```

---

## ACID Properties

Transactions must follow **ACID rules**:

### A — Atomicity

“All or nothing”

* Either the whole transaction happens
* Or nothing happens

---

### C — Consistency

* Database moves from one valid state to another
* Rules and constraints must not be broken

---

### I — Isolation

* Transactions should not interfere with each other
* Each transaction behaves as if it runs alone

---

### D — Durability

* Once committed, changes are permanent
* Data is not lost even after system failure

---

## Concurrency Control

**Concurrency control** manages multiple transactions running at the same time.

### Goal:

Prevent transactions from interfering with each other.

---

## Why Concurrency is Needed

* Many users access database at same time
* Improves performance
* But can cause errors if not controlled

---

## Problems in Concurrency

### 1. Lost Update Problem

One transaction overwrites another update.

```text id="c1"
T1 reads balance = 100
T2 reads balance = 100

T1 adds +50 → 150
T2 adds +20 → 120 (overwrites T1)

Final result incorrect
```

---

### 2. Uncommitted Dependency (Dirty Read)

Reading data that has not been committed.

```text id="c2"
T1 updates balance = 200 (not committed)
T2 reads 200
T1 aborts → balance returns to 100

T2 used wrong value
```

---

### 3. Inconsistent Analysis Problem

One transaction reads data while another is updating it.

```text id="c3"
T5 transfers money between accounts
T6 calculates total balance

T6 reads mixed old + new values → wrong total
```

---

## Schedule

A **schedule** is the order in which transaction operations are executed.

### Serial Schedule

* One transaction at a time
* No overlap

```text id="s1"
T1 → finish → T2 → finish → T3
```

### Non-Serial Schedule

* Transactions are interleaved

```text id="s2"
T1 read
T2 read
T1 write
T2 write
```

---

## Serializability

A schedule is **serializable** if:

* It produces the same result as a serial schedule

### Goal:

Allow concurrency but still keep correctness.

---

## Conflicts in Transactions

Operations conflict if:

* One writes and another reads same data
* Both write same data

No conflict if:

* Both only read
* Different data items

---

## Concurrency Control Techniques

### 1. Locking (Most common)

Transactions lock data before using it.

### Types of Locks:

#### Shared Lock (Read lock)

* Multiple transactions can read
* No updates allowed

#### Exclusive Lock (Write lock)

* Only one transaction allowed
* Read + write allowed

```text id="lock1"
Shared → multiple readers
Exclusive → one writer only
```

---

## Two-Phase Locking (2PL)

Ensures serializability.

### Two phases:

#### 1. Growing phase

* Acquire locks only
* No releasing allowed

#### 2. Shrinking phase

* Release locks only
* No new locks allowed

```text id="2pl"
Grow → Lock items
Shrink → Unlock items
```

### Important:

* Ensures correctness
* Can cause deadlocks
* Reduces parallelism

---

## 2. Timestamping

* Each transaction gets a timestamp
* Order of execution is based on time order
* No locks needed

---

## Optimistic Control

* Assumes conflicts are rare
* Transactions execute freely
* Checked only at commit time

---

# Recovery

## What is Recovery?

Recovery restores database after failure.

---

## Why Recovery is Needed

Failures may occur due to:

* System crash
* Power failure
* Hardware failure
* Software errors
* Human mistakes
* Natural disasters

---

## Storage Types

### Volatile Storage

* Temporary (RAM)
* Lost on crash

### Non-Volatile Storage

* Permanent (disk)
* Survives crashes

---

## Transaction Recovery Role

Recovery manager ensures:

* Atomicity (undo incomplete transactions)
* Durability (redo committed transactions)

---

## Recovery Actions

### Undo (Rollback)

* Remove effects of incomplete transactions

### Redo (Rollforward)

* Reapply committed transactions not saved to disk

```text id="rec1"
Crash happens
→ Undo incomplete transactions
→ Redo committed transactions
```

---

## Logging

A **log** records all database changes.

It includes:

* Transaction ID
* Operation type (insert/update/delete)
* Before image
* After image

```text id="log1"
T1: UPDATE balance
Before: 100
After: 150
```

---

## Checkpoint

A **checkpoint** is a save point in the database.

### Purpose:

* Reduce recovery time
* Mark consistent state

### Process:

* Write all data to disk
* Record active transactions

```text id="cp1"
Database state saved → checkpoint created
```

---

## Recovery Using Checkpoints

After a crash:

### Step 1: Redo

* Transactions committed after checkpoint

### Step 2: Undo

* Transactions not completed at crash time

```text id="cp2"
Checkpoint at tc

Redo: committed after tc
Undo: incomplete at crash
```

---

## Simple Summary

### Transaction

```text id="sum1"
Work unit in database
→ Commit or Rollback
```

---

### ACID

```text id="sum2"
A = All or nothing
C = Valid state
I = No interference
D = Permanent changes
```

---

### Concurrency Problems

* Lost update
* Dirty read
* Inconsistent analysis

---

### Control Methods

* Locking (2PL)
* Timestamping
* Optimistic control

---

### Recovery Tools

* Logs
* Checkpoints
* Undo / Redo

---

## Final Exam Memory Aid

```text id="final1"
Transaction = Unit of work

Commit = Save permanently
Rollback = Undo changes

Locking = Prevent conflict
2PL = Safe locking rule

Recovery = Fix after crash
Log = Record changes
Checkpoint = Save point
```
---
# Chap 10
Normalization, Denormalization, and Partitioning

## Normalization (Quick idea)

Normalization is the process of organizing database tables to:

* reduce redundancy (duplicate data)
* improve consistency
* avoid update anomalies

### Result of normalization

* Clean structure
* Minimal redundancy
* Data is logically organized

---

## Problem with full normalization

Even though normalization is good for design:

* Too many tables can be created
* Queries may need many JOIN operations
* Performance may become slower

So sometimes:

* We sacrifice some normalization for better performance

---

# Denormalization

## Meaning

Denormalization is when we intentionally:

* reduce the level of normalization
* or combine tables to improve performance

It usually means:

* adding redundancy on purpose

---

## Why denormalization is used

Main goal:

* improve query performance (especially reads)

But trade-offs include:

* slower updates
* more storage used
* more complexity in maintenance
* higher risk of inconsistency

---

## Key idea

```text id="d1"
Normalization → clean design
Denormalization → faster access (but messy data)
```

---

## Effects of denormalization

### Advantages

* Fewer joins needed
* Faster data retrieval
* Better performance for read-heavy systems

### Disadvantages

* More duplicate data
* Harder to maintain
* Slower inserts/updates/deletes
* Risk of data inconsistency

---

## When denormalization is used

Used mainly when performance is important, such as:

* frequent queries
* reporting systems
* real-time applications
* critical transactions

---

## Common denormalization techniques

### 1. Combining 1:1 relationships

* Merge two tables into one
* Reduces joins

---

### 2. Duplicating attributes in 1:M relationships

* Copy non-key attributes into multiple tables
* Reduces need for joins

---

### 3. Duplicating foreign keys

* Store foreign key in multiple places
* Faster access but increases redundancy

---

### 4. Introducing repeating groups

* Store multiple values in one row (not ideal in strict normalization)
* Improves read speed but reduces structure quality

---

### 5. Partitioning relations (sometimes mixed approach)

* Split or reorganize tables for performance
* Can be horizontal or vertical partitioning

---

# Partitioning (Alternative to denormalization)

Instead of combining tables, we split them into smaller parts.

## Why partitioning is used

* improve performance
* make data easier to manage
* improve scalability

---

## Types of partitioning

### 1. Horizontal Partitioning

* Split table by rows
* Each partition has same columns

Example:

* Customers split by region

  * Malaysia customers
  * Singapore customers

```text id="p1"
Same columns → fewer rows per table
```

---

### 2. Vertical Partitioning

* Split table by columns
* Each partition has same rows

Example:

* Customer basic info in one table
* Customer financial info in another

```text id="p2"
Same rows → fewer columns per table
```

---

## Denormalization vs Partitioning

| Concept         | What it does              | Goal                                |
| --------------- | ------------------------- | ----------------------------------- |
| Normalization   | Splits tables             | Reduce redundancy                   |
| Denormalization | Combines tables           | Improve speed                       |
| Partitioning    | Splits tables differently | Improve performance & manageability |

### Advantages and disadvantages of denormalization
| Advantages | Disadvantages |
|------------|---------------|
| **Can improve performance by:** | May speed up retrievals but can slow down updates. |
| - Precomputing derived data | Always application-specific and needs to be re-evaluated if the application changes. |
| - Minimizing the need for joins | Can increase the size of relations. |
| - Reducing the number of foreign keys in relations | May simplify implementation in some cases but may make it more complex in others. |
| - Reducing the number of indexes (thereby saving storage space) | Sacrifices flexibility. |
| - Reducing the number of relations |  |

---

## Simple exam summary

```text id="s1"
Normalization → remove redundancy
Denormalization → add redundancy for speed
Partitioning → split data for performance
```

---

## Final memory points

* Normalized design = clean but may be slow
* Denormalized design = faster reads but more redundancy
* Partitioning = performance improvement by splitting data
* Denormalization is used only when performance is critical
* Always balance design vs efficiency


--- 
# Chap 11
Data Warehouse

## Definition

A **data warehouse** is a special database used for **decision support and analysis**, not daily transactions.

It is:

* Separate from operational databases
* Designed for analysis and reporting
* Built using historical and integrated data

---

## Simple idea

```text id="dw1"
Operational DB → runs daily business
Data Warehouse → helps make decisions
```

---

## Inmon definition (important)

A data warehouse is:

* Subject-oriented
* Integrated
* Time-variant
* Non-volatile

---

## Key Characteristics

### 1. Subject-oriented

* Organized around key business topics
* Example:

  * Customers
  * Sales
  * Products

---

### 2. Integrated

* Combines data from multiple sources

* Example sources:

  * Databases
  * Excel files
  * Transaction systems

* Data is cleaned and standardized:

  * same formats
  * same naming rules
  * consistent values

---

### 3. Time-variant

* Stores historical data
* Used to analyze trends over time
* Usually covers long periods (e.g. 5–10 years)

---

### 4. Non-volatile

* Data is not updated or deleted frequently
* Only:

  * loaded
  * queried

No normal transaction updates like OLTP systems

---

## Purpose of Data Warehouses

Used for:

* business analysis
* decision making
* trend analysis

---

## Example Uses

### Customer analysis

* buying patterns
* spending habits
* purchase timing

---

### Product analysis

* sales performance
* product comparison
* regional performance

---

## Data Warehouse vs Operational Database

### OLTP vs OLAP

| Feature     | OLTP               | OLAP                 |
| ----------- | ------------------ | -------------------- |
| Purpose     | Daily transactions | Analysis & decisions |
| Users       | Clerks, staff      | Managers, analysts   |
| Data        | Current data       | Historical data      |
| Query type  | Simple             | Complex              |
| Speed focus | Fast transactions  | Fast analysis        |
| Data size   | Smaller            | Very large           |
| Usage       | Repeated tasks     | Ad-hoc queries       |

---

## Key difference idea

```text id="dw2"
OLTP → “Do transactions”
OLAP → “Analyze data”
```

---

## Data Warehouse Properties

* No frequent updates
* No transaction processing
* No concurrency control needed like OLTP
* Only:

  * initial loading
  * querying

---

## Data Warehouse Architecture

Data comes from multiple sources:

* operational databases
* flat files
* external systems

Then it is:

1. Extracted
2. Cleaned
3. Transformed
4. Loaded (ETL process)

---

## Data Cube Concept

A data warehouse uses a **multidimensional model** called a data cube.

### Example dimensions:

* Time (day, month, year)
* Product
* Region

### Measures:

* sales amount
* quantity sold

---

## Data Cube Structure

### Fact Table

* Central table
* Stores measurements (facts)
* Links to dimensions

Example:

* sales_amount
* quantity_sold

---

### Dimension Tables

Describe “context” of facts:

* Product (name, brand, type)
* Time (day, month, year)
* Location (city, region)

---

## Schema Types

### 1. Star Schema (most common)

* One fact table in the center
* Dimension tables around it

```text id="dw3"
      Time
       |
Product—Fact—Location
```

* Simple and fast
* No normalization in dimensions

---

### 2. Snowflake Schema

* Extension of star schema
* Dimension tables are normalized
* More complex structure

```text id="dw4"
Dimension → split into sub-dimensions
```

* Saves space
* More joins needed

---

### 3. Fact Constellation (Galaxy Schema)

* Multiple fact tables
* Shared dimension tables

Example:

* sales fact table
* shipping fact table

---

## Key Difference: OLTP vs Data Warehouse

### Operational system (OLTP)

* Current data
* Fast updates
* Day-to-day operations

### Data warehouse (OLAP)

* Historical data
* Analytical queries
* Decision support

---

## Why Data Warehouses are useful

* Understand customer behaviour
* Track business trends
* Compare performance over time
* Improve decision making

---

## Simple exam summary

```text id="dw5"
Data Warehouse:
→ Subject-oriented
→ Integrated
→ Historical
→ Read-only

Used for:
→ Analysis
→ Decision making
```

---

## Final memory aid

```text id="dw6"
OLTP = run business
OLAP = analyze business

Warehouse = historical + integrated + reporting
```
