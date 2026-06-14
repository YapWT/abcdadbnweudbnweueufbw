# Q1: What is the problem with ER model? Identify and explain them.

## Answer:
Some limitations/problems of the ER (Entity-Relationship) Model are:

1. **Limited Semantic Representation**
   - ER models cannot represent all real-world constraints and business rules.
   - Example: A student must enroll in at least one course cannot be fully enforced in a basic ER diagram.

2. **Complexity in Large Databases**
   - Large systems may produce very complex ER diagrams that are difficult to understand and maintain.

3. **No Representation of Operations**
   - ER models describe data structures but do not show how data is processed or manipulated.

4. **Difficulty Representing Time-Dependent Data**
   - ER models do not naturally represent historical or temporal information.

---

# Q2: What is the difference between specialization hierarchy and generalization hierarchy?

## Answer:

| Specialization Hierarchy | Generalization Hierarchy |
|-------------------------|--------------------------|
| Top-down approach. | Bottom-up approach. |
| Starts with a general entity and creates specialized entities. | Starts with several entities and combines them into a generalized entity. |
| More specific entities inherit attributes from the parent entity. | Common attributes are extracted into a parent entity. |
| Example: Employee → Manager, Engineer. | Example: Car, Truck → Vehicle. |

---

# Q3: What is inheritance in ER model?

## Answer:
Inheritance is the property where a subclass automatically acquires the attributes and relationships of its superclass.

### Example:
- Superclass: Employee(EmployeeID, Name)
- Subclass: Manager(Bonus)

The Manager entity inherits EmployeeID and Name from Employee and adds Bonus.

### Benefits:
- Reduces redundancy.
- Improves data consistency.
- Simplifies database design.

---

# Q4: What are the advantages of using stored procedure?

## Answer:

1. **Improves Performance**
   - Stored procedures are precompiled and execute faster.

2. **Enhances Security**
   - Users can execute procedures without direct access to tables.

3. **Reduces Network Traffic**
   - Multiple SQL statements can be executed with a single procedure call.

4. **Code Reusability**
   - Same procedure can be used by multiple applications.

5. **Easier Maintenance**
   - Business logic is centralized in the database.

---

# Q5: What is the difference between stored procedure and trigger?

## Answer:

| Stored Procedure | Trigger |
|------------------|----------|
| Executed manually or called by an application. | Executed automatically when an event occurs. |
| Can accept parameters. | Cannot be directly executed by users. |
| Used for business logic and repetitive tasks. | Used for automatic enforcement of rules. |
| Invoked using EXEC command. | Invoked automatically by INSERT, UPDATE, DELETE events. |

---

# Q6: Give three responsibilities of a DA (Data Administrator).

## Answer:

1. Develop data policies and standards.
2. Define enterprise-wide data requirements.
3. Ensure data quality and consistency across the organization.

---

# Q7: Give three responsibilities of a DBA (Database Administrator).

## Answer:

1. Manage database security and user access.
2. Perform database backup and recovery.
3. Monitor and optimize database performance.

---

# Q8: Give three examples of data backup and recovery.

## Answer:

1. **Full Backup**
   - Copies the entire database.

2. **Incremental Backup**
   - Copies only data changed since the last backup.

3. **Differential Backup**
   - Copies all changes since the last full backup.

---

# Q9: Differentiate three responsibilities between DA and DBA.

## Answer:

| Data Administrator (DA) | Database Administrator (DBA) |
|------------------------|------------------------------|
| Focuses on data planning and policies. | Focuses on technical database management. |
| Defines data standards. | Implements database security and maintenance. |
| Concerned with organizational data requirements. | Concerned with database performance and operations. |

---

# Q10: Provide three reasons why we need to implement database security. Explain with examples.

## Answer:

### 1. Protect Confidential Information
- Prevent unauthorized access to sensitive data.
- Example: Employee salary records should only be viewed by HR staff.

### 2. Maintain Data Integrity
- Prevent unauthorized modifications.
- Example: Students should not be able to change their own examination results.

### 3. Ensure Data Availability
- Protect data from accidental loss or cyberattacks.
- Example: Regular backups help recover customer data after a system crash.

---

# Q11: Explain properties of transactions.

## Answer:

Transactions follow the ACID properties:

### 1. Atomicity
- All operations are completed or none are completed.

### 2. Consistency
- Database remains in a valid state before and after transaction.

### 3. Isolation
- Concurrent transactions do not interfere with each other.

### 4. Durability
- Committed changes remain permanently even after system failure.

---

# Q12: What are the problems caused by concurrency? Explain with examples.

## Answer:

### 1. Lost Update
- Two transactions update the same data and one update is overwritten.

**Example:**
- T1 updates balance from 100 to 120.
- T2 updates balance from 100 to 85.
- Final balance becomes 85, losing T1's update.

### 2. Dirty Read
- A transaction reads uncommitted data from another transaction.

### 3. Unrepeatable Read
- A transaction reads the same data twice but gets different results because another transaction modified it.

---

# Q13: Explain two basic concurrency control techniques.

## Answer:

### 1. Lock-Based Concurrency Control
- Transactions lock data before accessing it.
- Prevents multiple conflicting operations.

### 2. Timestamp-Based Concurrency Control
- Each transaction receives a timestamp.
- Transactions execute according to timestamp order.

---

# Q14: Explain two phases for transactions.

## Answer:

### 1. Read Phase
- Transaction reads data and performs calculations.

### 2. Write Phase
- Transaction updates the database and commits changes.

---

# Q15: Explain three types of failures.

## Answer:

### 1. Transaction Failure
- Transaction cannot complete successfully.
- Example: Invalid input data.

### 2. System Failure
- Hardware or software crash causes interruption.
- Example: Power outage.

### 3. Media Failure
- Physical storage device failure.
- Example: Hard disk crash.

---
# Q16(a): Given the authorization table below, write SQL statements to grant access rights to each user on the Employee table.

## Authorization Table

| Privilege | David | Emma | Farah |
|------------|--------|--------|--------|
| SELECT | YES | YES | NO |
| INSERT | YES | NO | YES |
| UPDATE | NO | YES | YES |
| DELETE | NO | YES | NO |
| GRANT | YES | NO | NO |

## Answer:

### Grant privileges to David
```sql
GRANT SELECT, INSERT
ON Employee
TO David
WITH GRANT OPTION;
````

### Grant privileges to Emma

```sql
GRANT SELECT, UPDATE, DELETE
ON Employee
TO Emma;
```

### Grant privileges to Farah

```sql
GRANT INSERT, UPDATE
ON Employee
TO Farah;
```

---

# Q16(b): Revoke the following privileges from the users.

## Requirements

| User  | Privilege to Revoke From Employee Table |
| ----- | --------------------------------------  |
| David | INSERT                                  |
| Emma  | DELETE                                  |

## Answer:

### Revoke INSERT privilege from David

```sql
REVOKE INSERT
ON Employee
FROM David;
```

### Revoke DELETE privilege from Emma

```sql
REVOKE DELETE
ON Employee
FROM Emma;
```

```

### Explanation
- `WITH GRANT OPTION` is used for **David** because he has **GRANT = YES**, allowing him to grant his privileges to other users.
- Emma and Farah do not have GRANT permission, so `WITH GRANT OPTION` is not included.
- `REVOKE` removes the specified privilege from the user while leaving other privileges unchanged.
```

---

# Q17b: Consider the interleaved transaction schedule below which suffers from a concurrency control problem: 

| Time | Transaction 1     | Transaction 2     | Balance (Z) |
| ---- | ----------------- | ----------------- | ----------- |
| 1    | begin_transaction |                   | 100         |
| 2    | read(Z)           |                   | 100         |
| 3    |                   | begin_transaction | 100         |
| 4    |                   | read(Z)           | 100         |
| 5    | Z = Z + 20        | ...               | 100         |
| 6    |                   | Z = Z - 15        | 100         |
| 7    | write(Z)          | ...               | 120         |
| 8    | commit            | ...               | 120         |
| 9    |                   | write(Z)          | 85          |
| 10   |                   | commit            | 85          |

---

## Q17(B1): Identify the concurrency control problem shown in the schedule above.

### Answer:

The concurrency control problem is **Lost Update**.

### Explanation:

* Initial balance Z = 100.
* Transaction 1 reads Z = 100 and calculates:

  * Z = 100 + 20 = 120
* Transaction 2 also reads Z = 100 and calculates:

  * Z = 100 − 15 = 85
* Transaction 1 writes 120 and commits.
* Transaction 2 then writes 85 using the old value it read earlier (100).

As a result, Transaction 2 overwrites Transaction 1's update.

### Expected Result:

```
100 + 20 - 15 = 105
```

### Actual Result:

```
85
```

The update made by Transaction 1 is lost, therefore this is called a **Lost Update Problem**.

---

## Q17(B2): Suggest one concurrency control technique that can prevent this problem.

### Answer:

**Two-Phase Locking (2PL) using an Exclusive Lock (X-Lock)**

### Explanation:

* Before updating Balance (Z), a transaction must obtain an **exclusive lock** on Z.
* While Transaction 1 holds the lock, Transaction 2 must wait.
* After Transaction 1 commits and releases the lock, Transaction 2 can access and update the latest value.

### Example:

1. T1 obtains Exclusive Lock on Z.
2. T1 updates Z from 100 to 120 and commits.
3. T1 releases the lock.
4. T2 reads updated value 120.
5. T2 updates Z to 105 and commits.

### Correct Final Balance:

```
100 + 20 - 15 = 105
```

Thus, **Two-Phase Locking (2PL)** prevents the Lost Update problem and ensures data consistency.

---

# Q18: Explain and differentiate shared and exclusive lock.

## Answer:

| Shared Lock (S)                                             | Exclusive Lock (X)                               |
| ----------------------------------------------------------- | ------------------------------------------------ |
| Used for reading data.                                      | Used for updating data.                          |
| Multiple transactions can hold shared locks simultaneously. | Only one transaction can hold an exclusive lock. |
| Does not allow writing.                                     | Prevents other reads and writes.                 |

### Example:

* Shared Lock: Multiple users viewing account details.
* Exclusive Lock: One user updating account balance.

---

# Q19: Explain denormalization.

## Answer:

Denormalization is the process of intentionally adding redundant data into a database to improve query performance.

### Advantages:

* Faster query execution.
* Fewer table joins.

### Disadvantages:

* Increased storage usage.
* Possibility of data inconsistency.

### Example:

Store CustomerName directly in the Orders table to avoid frequent joins with Customers table.

---

# Q20: Explain horizontal and vertical partitioning.

## Answer:

### Horizontal Partitioning

* Divides a table by rows.

**Example:**

* Customer table split by region:

  * Asia Customers
  * Europe Customers

### Vertical Partitioning

* Divides a table by columns.

**Example:**

* Employee table:

  * Employee(EmployeeID, Name)
  * EmployeeDetails(EmployeeID, Salary, Address)

### Difference

| Horizontal Partitioning                   | Vertical Partitioning                     |
| ----------------------------------------- | ----------------------------------------- |
| Splits rows.                              | Splits columns.                           |
| Same columns in each partition.           | Same primary key in each partition.       |
| Used for large datasets across locations. | Used to improve performance and security. |

---

# Q21: Consider the following tables which show the payment records made by customers.

## Table Name: Customers

| CustomerID | CustomerName | ContactPerson |
|------------|-------------|--------------|
| C101 | Fresh Valley Mart | Ravi Kumar |
| C102 | Green Basket Store | Nur Aisyah |
| C103 | Daily Needs Shop | Lim Wei |

## Table Name: Payments

| PaymentID | CustomerID | PaymentType | PaymentDate | Status | PaymentRef |
|------------|------------|-------------|-------------|---------|------------|
| P901 | C101 | Online Banking | 2024-01-12 | Completed | P901 |
| P902 | C101 | Credit Card | 2024-02-18 | Pending | P902 |
| P903 | C102 | Cash | 2023-11-25 | Completed | P903 |
| P904 | C103 | Online Banking | 2024-03-08 | Failed | P904 |

---

# Q21(a): Based on the tables above, create a stored procedure to count how many 'Pending' payments are associated with a particular contact person.

## Answer:

```sql
DELIMITER $$

CREATE PROCEDURE CountPendingPayments(
    IN p_ContactPerson VARCHAR(100)
)
BEGIN
    SELECT COUNT(*) AS PendingPaymentCount
    FROM Customers C
    JOIN Payments P
        ON C.CustomerID = P.CustomerID
    WHERE C.ContactPerson = p_ContactPerson
      AND P.Status = 'Pending';
END$$

DELIMITER ;
```

### Example Execution

```sql
CALL CountPendingPayments('Ravi Kumar');
```

### Expected Result

| PendingPaymentCount |
|---------------------|
| 1 |

---

# Q21(b): Based on the tables above, create a trigger to prevent the deletion of a payment record. Instead, change the payment status to 'CANCELLED'.

## Answer:

```sql
DELIMITER $$

CREATE TRIGGER PreventPaymentDelete
BEFORE DELETE
ON Payments
FOR EACH ROW
BEGIN
    SIGNAL SQLSTATE '45000'
    SET MESSAGE_TEXT =
    'Deletion is not allowed. Change payment status to CANCELLED instead.';
END$$

DELIMITER ;
```

### To cancel a payment instead of deleting it:

```sql
UPDATE Payments
SET Status = 'CANCELLED'
WHERE PaymentID = 'P901';
```

### Example Result

Before:

| PaymentID | Status |
|------------|---------|
| P901 | Completed |

After:

| PaymentID | Status |
|------------|---------|
| P901 | CANCELLED |

---

# Q21(c): Give two advantages of triggers.

## Answer:

### 1. Automatic Enforcement of Business Rules
Triggers execute automatically whenever a specified database event occurs (INSERT, UPDATE, DELETE).

**Example:**
A trigger can prevent users from deleting payment records and ensure that records are only marked as 'CANCELLED'.

### 2. Maintains Data Integrity and Consistency
Triggers help ensure that database rules are followed automatically.

**Example:**
Whenever a payment record is updated, a trigger can automatically record the changes in an audit table to maintain accurate transaction history.


