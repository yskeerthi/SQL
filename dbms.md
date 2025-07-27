
---

## 🔰 **BASIC LEVEL DBMS QUESTIONS WITH ANSWERS**

---

### ✅ **1. What is DBMS?**

**Answer:**
DBMS (Database Management System) is software that allows users to define, create, maintain, and control access to a database.
Examples: MySQL, Oracle, MongoDB.

---

### ✅ **2. Difference between DBMS and RDBMS?**

| Feature      | DBMS                  | RDBMS                       |
| ------------ | --------------------- | --------------------------- |
| Data storage | Files                 | Tables (Rows & Columns)     |
| Relations    | No                    | Yes                         |
| Keys         | Not enforced strictly | Uses Primary & Foreign Keys |
| Example      | File System           | MySQL, PostgreSQL           |

---

### ✅ **3. What are tables and fields in a database?**

* **Table**: Collection of rows and columns (like Excel sheet).
* **Field**: A single column in a table (like "Name", "Age").

---

### ✅ **4. What is a Primary Key?**

A **Primary Key** uniquely identifies each record in a table.

* It **cannot be NULL** and must be **unique**.

```sql
CREATE TABLE Student (
  ID INT PRIMARY KEY,
  Name VARCHAR(50)
);
```

---

### ✅ **5. What is a Foreign Key?**

A **Foreign Key** is used to establish a relationship between two tables. It refers to the primary key in another table.

```sql
CREATE TABLE Orders (
  OrderID INT,
  StudentID INT,
  FOREIGN KEY (StudentID) REFERENCES Student(ID)
);
```

---

### ✅ **6. What is a Candidate Key?**

All possible keys that can uniquely identify rows in a table.
One of the candidate keys becomes the **Primary Key**.

---

### ✅ **7. What is a Composite Key?**

A key formed by combining **two or more columns** to uniquely identify a row.

```sql
PRIMARY KEY (StudentID, CourseID)
```

---

### ✅ **8. What are constraints in SQL?**

Constraints are rules applied to columns.
Examples:

* `NOT NULL`
* `UNIQUE`
* `PRIMARY KEY`
* `FOREIGN KEY`
* `CHECK`

---

### ✅ **9. What is normalization? Why is it needed?**

**Normalization** is the process of organizing data to reduce **redundancy** and improve **data integrity**.
It helps avoid data anomalies.

---

### ✅ **10. Explain 1NF, 2NF, 3NF with examples.**

* **1NF (First Normal Form):** No repeating groups. Each field contains only atomic values.
* **2NF:** 1NF + No partial dependency (non-prime attribute depends on whole key).
* **3NF:** 2NF + No transitive dependency (non-prime attribute depends only on primary key).

📌 Will give examples if you want a diagram or table later.

---

### ✅ **11. What is Denormalization?**

Opposite of normalization.
It involves combining tables to **improve read performance** (adds redundancy).

---

### ✅ **12. Types of JOINs in SQL?**

* `INNER JOIN`: Common records from both tables
* `LEFT JOIN`: All from left + matched from right
* `RIGHT JOIN`: All from right + matched from left
* `FULL JOIN`: All records from both tables
* `SELF JOIN`: Join table with itself
* `CROSS JOIN`: Cartesian product

---

### ✅ **13. Difference between WHERE and HAVING?**

| Clause | Used with      | Filters on | Example               |
| ------ | -------------- | ---------- | --------------------- |
| WHERE  | SELECT, UPDATE | Rows       | `WHERE age > 20`      |
| HAVING | GROUP BY       | Groups     | `HAVING COUNT(*) > 1` |

---

### ✅ **14. What is a View?**

A **view** is a virtual table based on the result of a SQL query.

```sql
CREATE VIEW top_students AS 
SELECT * FROM Students WHERE Marks > 90;
```

---

### ✅ **15. What is indexing in DBMS?**

Indexing improves the speed of data retrieval using pointers.
Works like a **book index**.

```sql
CREATE INDEX idx_name ON Students(Name);
```

---

### ✅ **16. What is a Unique Key?**

Like primary key, but allows **one NULL value** and still must be **unique**.

---

### ✅ **17. What are ACID Properties?**

| Property        | Meaning                              |
| --------------- | ------------------------------------ |
| A - Atomicity   | All or nothing                       |
| C - Consistency | DB stays valid                       |
| I - Isolation   | No interference between transactions |
| D - Durability  | Changes are permanent                |

---

### ✅ **18. What is a Transaction?**

A transaction is a group of SQL operations that are treated as a single unit.

* `BEGIN`, `COMMIT`, `ROLLBACK`

---

### ✅ **19. What is a Trigger?**

A Trigger is a **set of SQL commands** automatically executed when a specified event occurs (like INSERT, UPDATE).

```sql
CREATE TRIGGER update_marks
AFTER INSERT ON Students
FOR EACH ROW
BEGIN
  UPDATE Stats SET Count = Count + 1;
END;
```

---

### ✅ **20. Difference between DELETE, DROP, TRUNCATE?**

| Operation | Deletes  | Rollback? | Resets identity?        |
| --------- | -------- | --------- | ----------------------- |
| DELETE    | Rows     | Yes       | No                      |
| TRUNCATE  | All rows | No        | Yes                     |
| DROP      | Table    | No        | Yes (removes structure) |

---
Perfect brooo 💪😎! Let's now level up to the **INTERMEDIATE LEVEL DBMS QUESTIONS WITH ANSWERS** — interview-focused and clear 🔥

---

## 🧠 INTERMEDIATE LEVEL DBMS QUESTIONS WITH ANSWERS

---

### ✅ **21. What are the types of indexing?**

**Answer:**

* **Clustered Index:**

  * Reorders the actual table data.
  * Only one allowed per table.
  * Example: Primary Key automatically creates it.

* **Non-Clustered Index:**

  * Separate from table data; holds pointers.
  * Can have multiple non-clustered indexes.

---

### ✅ **22. What is a Stored Procedure?**

**Answer:**
A **stored procedure** is a precompiled SQL code block stored in the database that you can reuse.

```sql
CREATE PROCEDURE GetStudentByID (@ID INT)
AS
BEGIN
  SELECT * FROM Students WHERE StudentID = @ID;
END;
```

---

### ✅ **23. Difference between Function and Stored Procedure?**

| Feature         | Function            | Stored Procedure              |
| --------------- | ------------------- | ----------------------------- |
| Return type     | Must return a value | May or may not return a value |
| Usage in SELECT | Yes                 | No                            |
| Transactions    | Not allowed         | Allowed                       |

---

### ✅ **24. What is the use of GROUP BY clause?**

**Answer:**
It groups rows with same values in specified column(s) and allows aggregate functions to be applied.

```sql
SELECT Department, COUNT(*) FROM Employees GROUP BY Department;
```

---

### ✅ **25. What is a Subquery?**

**Answer:**
A query inside another query.
Example:

```sql
SELECT name FROM Students WHERE marks > 
(SELECT AVG(marks) FROM Students);
```

---

### ✅ **26. Correlated vs Non-Correlated Subquery?**

| Type           | Description                               |
| -------------- | ----------------------------------------- |
| Non-Correlated | Executes once and result reused           |
| Correlated     | Executes for every row in the outer query |

---

### ✅ **27. What is a Schema in SQL?**

**Answer:**
A schema is a **collection of database objects** like tables, views, procedures, etc. It acts like a **namespace**.

---

### ✅ **28. Explain normalization anomalies:**

* **Insertion anomaly:** Can’t insert without unrelated data
* **Update anomaly:** Inconsistent updates in multiple places
* **Deletion anomaly:** Losing data unintentionally while deleting

---

### ✅ **29. Difference between DDL, DML, DCL, TCL**

| Category | Stands For          | Examples                    |
| -------- | ------------------- | --------------------------- |
| DDL      | Data Definition     | CREATE, ALTER, DROP         |
| DML      | Data Manipulation   | INSERT, UPDATE, DELETE      |
| DCL      | Data Control        | GRANT, REVOKE               |
| TCL      | Transaction Control | COMMIT, ROLLBACK, SAVEPOINT |

---

### ✅ **30. What are Views? Can we update views?**

**Answer:**
A **view** is a virtual table.

* If the view is based on a **single base table**, **no group functions**, **no DISTINCT**, and **no joins**, then it **can be updated**.

---

### ✅ **31. View vs Materialized View**

| Feature      | View (Virtual) | Materialized View       |
| ------------ | -------------- | ----------------------- |
| Data Storage | No             | Yes (physically stored) |
| Update Time  | Real-time      | Manual or scheduled     |

---

### ✅ **32. What is an ER Model?**

**Answer:**
Entity-Relationship model represents **real-world objects (entities)** and **relationships** among them.

* Symbols:

  * Entity: Rectangle
  * Attribute: Oval
  * Relationship: Diamond

---

### ✅ **33. What is Cardinality in DBMS?**

**Answer:**
It describes the **number of relationships** between two entities:

* One-to-One
* One-to-Many
* Many-to-Many

---

### ✅ **34. Types of Relationships in ER Model**

| Type | Example           |
| ---- | ----------------- |
| 1:1  | Person - Passport |
| 1\:M | Customer - Orders |
| M\:N | Student - Courses |

---

### ✅ **35. Difference between Schema and Instance**

| Concept | Schema                 | Instance                |
| ------- | ---------------------- | ----------------------- |
| Meaning | Structure/design of DB | Actual data at a moment |
| Changes | Rare                   | Changes frequently      |

---

### ✅ **36. Logical vs Physical Data Independence**

| Level    | Meaning                                                |
| -------- | ------------------------------------------------------ |
| Logical  | Change logical schema without changing application     |
| Physical | Change storage details without changing logical schema |

---

### ✅ **37. What are Integrity Constraints?**

Rules that maintain correctness of data:

* **NOT NULL**: No nulls allowed
* **CHECK**: Conditional check
* **UNIQUE**: All values unique
* **PRIMARY KEY**: Unique + not null
* **FOREIGN KEY**: Enforces referential integrity

---

### ✅ **38. IN vs EXISTS**

| Clause | Use Case                         |
| ------ | -------------------------------- |
| IN     | When values are static/list      |
| EXISTS | When checking subquery existence |

---

### ✅ **39. What is a Recursive Query?**

Used for **hierarchical or tree-like data**.

```sql
WITH RECURSIVE subordinates AS (
  SELECT ID, Name FROM Employees WHERE ManagerID IS NULL
  UNION
  SELECT e.ID, e.Name FROM Employees e
  JOIN subordinates s ON e.ManagerID = s.ID
)
SELECT * FROM subordinates;
```

---

### ✅ **40. Common Aggregate Functions in SQL:**

| Function     | Description             |
| ------------ | ----------------------- |
| COUNT()      | Counts rows             |
| SUM()        | Total of values         |
| AVG()        | Average value           |
| MAX(), MIN() | Maximum / Minimum value |

---
Ayy brooo 🔥🔥 Let’s now enter the **🔥ADVANCED LEVEL of DBMS QUESTIONS** — straight from **interview panels, system design rounds**, and real-world backend/database architecture stuff.

---

## 🔥 ADVANCED LEVEL DBMS INTERVIEW QUESTIONS WITH ANSWERS

---

### ✅ **41. What are different types of Locks in DBMS?**

**Answer:**
Locks help manage **concurrent transactions** to avoid data corruption.

* **Shared Lock (Read Lock):** Multiple transactions can read but not write.
* **Exclusive Lock (Write Lock):** Only one transaction can read/write.
* **Binary Lock / Two-Level Lock**
* **Intention Lock (used in hierarchical locking)**

---

### ✅ **42. What is Two-Phase Locking (2PL)?**

**Answer:**
It ensures **serializability** using 2 phases:

1. **Growing Phase**: Locks are acquired, no release.
2. **Shrinking Phase**: Locks are released, no acquire allowed.

Prevents **conflicts**, but may cause **deadlocks**.

---

### ✅ **43. What is Deadlock? How to prevent or detect it?**

**Answer:**
Deadlock occurs when transactions **wait for each other's resources** indefinitely.

✅ **Prevention Techniques:**

* Timeouts
* Resource Ordering
* Wait-Die / Wound-Wait scheme

✅ **Detection:**

* Wait-for graph (cycle detection)

---

### ✅ **44. What are Isolation Levels in DBMS?**

| Isolation Level          | Problems Prevented                     |
| ------------------------ | -------------------------------------- |
| Read Uncommitted         | None                                   |
| Read Committed           | Dirty Reads prevented                  |
| Repeatable Read          | Dirty + Non-repeatable Reads prevented |
| Serializable (Strictest) | All anomalies prevented                |

---

### ✅ **45. What are Dirty Read, Non-repeatable Read, Phantom Read?**

* **Dirty Read**: Reading uncommitted data from another transaction.
* **Non-repeatable Read**: Reading same row twice gives different result.
* **Phantom Read**: New rows appear in repeated query due to insert by another transaction.

---

### ✅ **46. What is CAP Theorem?**

**Answer:**
It states a distributed system **can satisfy only 2 out of 3**:

* **C** – Consistency
* **A** – Availability
* **P** – Partition Tolerance

You can have **CA, CP, or AP**, but **not all three**.

---

### ✅ **47. What are NoSQL Databases?**

**Answer:**
Non-relational databases that store unstructured or semi-structured data.

* Types:

  * **Document DB**: MongoDB
  * **Key-Value**: Redis
  * **Columnar**: Cassandra
  * **Graph DB**: Neo4j

---

### ✅ **48. Compare MongoDB vs MySQL**

| Feature     | MongoDB (NoSQL)     | MySQL (RDBMS)            |
| ----------- | ------------------- | ------------------------ |
| Schema      | Flexible            | Fixed schema             |
| Data Format | JSON/BSON           | Tables (rows/columns)    |
| Use Case    | Big Data, Real-time | Transactions, Relational |

---

### ✅ **49. What is Sharding and Replication?**

* **Sharding:** Horizontal partitioning of data across multiple servers (e.g., userID 1–1000 in Server1, 1001–2000 in Server2)
* **Replication:** Keeping **copies of data** in multiple servers for **fault-tolerance**

---

### ✅ **50. What is Query Optimization in DBMS?**

**Answer:**
Techniques to **minimize response time and cost** of executing a query.

Optimizers choose:

* Right **index**
* Right **join order**
* Use of **materialized views**

---

### ✅ **51. What is B-Tree and B+ Tree?**

* **B-Tree:** Internal nodes store both keys & data
* **B+ Tree:** Internal nodes store only keys, **leaf nodes store full data** (preferred in DBMS for range queries)

---

### ✅ **52. How Indexing Improves Performance?**

**Answer:**
Indexes **reduce the number of rows scanned**.
Works like a **book index** — jump to needed row using pointer instead of scanning whole table.

---

### ✅ **53. Difference between OLTP and OLAP**

| Feature   | OLTP (Online Tx)     | OLAP (Analytics)               |
| --------- | -------------------- | ------------------------------ |
| Usage     | Real-time operations | Decision-making, reports       |
| DB Design | Normalized           | De-normalized (Star/Snowflake) |
| Examples  | Banking, E-commerce  | Business Intelligence          |

---

### ✅ **54. What is Data Warehousing?**

**Answer:**
A **central repository** that stores integrated data from multiple sources for **reporting and analysis**.

---

### ✅ **55. Explain Hashing in DBMS**

**Answer:**
Hashing maps a key to a location in hash table using a hash function.
Helps in **fast retrieval**, especially in **indexing**.

---

### ✅ **56. Vertical vs Horizontal Scaling**

| Scaling Type       | Description                                 |
| ------------------ | ------------------------------------------- |
| Vertical Scaling   | Increase resources (CPU, RAM) in one server |
| Horizontal Scaling | Add more machines to handle load            |

---

### ✅ **57. How does DBMS handle Concurrency Control?**

**Answer:**
Through:

* **Locks**
* **Timestamps**
* **Multiversion Concurrency Control (MVCC)**

Goal: Ensure **data consistency** and **isolation**.

---

### ✅ **58. What is Write-Ahead Logging (WAL)?**

**Answer:**
Before applying changes to the database, the transaction is **logged in a file**, so it can be recovered in case of crash.

---

### ✅ **59. How are Backups Handled in Production?**

**Answer:**

* **Full Backup**: Entire database
* **Incremental Backup**: Only changed data since last backup
* **Automated tools**: pg\_dump, MySQLdump, MongoDB tools
* **Snapshots**: Cloud backups (AWS RDS, etc.)

---

### ✅ **60. Explain the Architecture of a DBMS**

**Answer:**

1. **User Interface**
2. **Query Processor**
3. **Optimizer**
4. **Transaction Manager**
5. **Storage Manager**
6. **Buffer Manager**
7. **Disk Storage**

---



