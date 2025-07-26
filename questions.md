Absolutely Keerthi! Here are **important and frequently asked SQL interview questions** – starting from basic to advanced – along with sample answers and tips for answering them confidently. 🌟

---

## ✅ BASIC LEVEL SQL INTERVIEW QUESTIONS

### 1. **What is SQL?**

**Answer**: SQL (Structured Query Language) is a language used to manage and manipulate relational databases.

---

### 2. **What are the types of SQL commands?**

**Answer**:

* **DDL** – Data Definition Language (`CREATE`, `ALTER`, `DROP`)
* **DML** – Data Manipulation Language (`INSERT`, `UPDATE`, `DELETE`)
* **DQL** – Data Query Language (`SELECT`)
* **DCL** – Data Control Language (`GRANT`, `REVOKE`)
* **TCL** – Transaction Control Language (`COMMIT`, `ROLLBACK`, `SAVEPOINT`)

---

### 3. **What is the difference between `WHERE` and `HAVING`?**

**Answer**:

* `WHERE` filters **before** grouping.
* `HAVING` filters **after** grouping.

---

### 4. **What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**

| Command  | Removes Data | Resets Auto ID | Can Rollback | Removes Table |
| -------- | ------------ | -------------- | ------------ | ------------- |
| DELETE   | Yes          | No             | Yes          | No            |
| TRUNCATE | Yes (All)    | Yes            | No           | No            |
| DROP     | Yes          | Yes            | No           | Yes           |

---

### 5. **What is the difference between `UNION` and `UNION ALL`?**

* `UNION`: Removes duplicates.
* `UNION ALL`: Keeps duplicates.

---

## 🧠 INTERMEDIATE LEVEL QUESTIONS

### 6. **What is a JOIN? Name types of JOINs.**

**Answer**:
A `JOIN` combines rows from two or more tables using a related column.

Types:

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL OUTER JOIN
* SELF JOIN
* CROSS JOIN

---

### 7. **What is normalization?**

**Answer**: Process of organizing data to reduce redundancy and improve data integrity.

Normal forms:

* 1NF – No repeating groups
* 2NF – No partial dependency
* 3NF – No transitive dependency

---

### 8. **What is a subquery?**

**Answer**: A query inside another query. It helps in filtering, computing or comparing values.

---

### 9. **What is the difference between `RANK()`, `DENSE_RANK()`, and `ROW_NUMBER()`?**

| Function       | Skips Rank? | Unique Row Number? |
| -------------- | ----------- | ------------------ |
| `RANK()`       | Yes         | No                 |
| `DENSE_RANK()` | No          | No                 |
| `ROW_NUMBER()` | N/A         | Yes                |

---

### 10. **What is a view in SQL?**

**Answer**: A virtual table based on the result of a query.

---

## 🚀 ADVANCED LEVEL QUESTIONS

### 11. **What is a CTE (Common Table Expression)?**

```sql
WITH TopStudents AS (
  SELECT * FROM students WHERE marks > 90
)
SELECT * FROM TopStudents;
```

Used for writing reusable and readable queries.

---

### 12. **What is indexing? How does it help performance?**

**Answer**: Indexing creates a quick lookup for specific columns and speeds up SELECT queries but slows down INSERT/UPDATE operations slightly.

---

### 13. **Explain ACID properties.**

* **A**tomicity: All or nothing
* **C**onsistency: Always valid data
* **I**solation: Transactions don’t interfere
* **D**urability: Committed data stays safe

---

### 14. **What is a trigger?**

**Answer**: A trigger automatically runs a block of code in response to events like `INSERT`, `UPDATE`, or `DELETE`.

---

### 15. **What are stored procedures?**

**Answer**: Precompiled SQL code that you can execute like a function with input/output parameters.

---

## 💼 PRACTICAL CODING QUESTIONS (Often Asked)

1. **Find second highest salary from employee table.**

```sql
SELECT MAX(salary) 
FROM employees 
WHERE salary < (SELECT MAX(salary) FROM employees);
```

2. **Find duplicates in a column.**

```sql
SELECT name, COUNT(*) 
FROM students 
GROUP BY name 
HAVING COUNT(*) > 1;
```

3. **Fetch top N rows per group (e.g., top 2 by marks per department).**

```sql
SELECT * FROM (
  SELECT *, RANK() OVER (PARTITION BY department ORDER BY marks DESC) as rnk
  FROM students
) t
WHERE rnk <= 2;
```

---
Absolutely Keerthi! Here's the **full Q\&A** for all **25 SQL interview questions**, including explanations and query examples where needed — great for interviews and real-time understanding. 💪🔥

---

## ✅ **25 SQL Interview Questions with Answers**

---

### 1. **What is SQL?**

**Answer**: SQL (Structured Query Language) is used to create, modify, query, and manage data in relational databases.

---

### 2. **What are the types of SQL commands?**

**Answer**:

* **DDL** (Data Definition): `CREATE`, `ALTER`, `DROP`
* **DML** (Data Manipulation): `INSERT`, `UPDATE`, `DELETE`
* **DQL** (Query): `SELECT`
* **DCL** (Control): `GRANT`, `REVOKE`
* **TCL** (Transaction): `COMMIT`, `ROLLBACK`, `SAVEPOINT`

---

### 3. **What is the difference between `WHERE` and `HAVING`?**

* `WHERE` filters rows **before** grouping.
* `HAVING` filters **after** grouping.

```sql
SELECT department, COUNT(*) 
FROM students 
GROUP BY department 
HAVING COUNT(*) > 1;
```

---

### 4. **What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**

| Command  | Removes Data | Resets ID? | Rollback? | Removes Table |
| -------- | ------------ | ---------- | --------- | ------------- |
| DELETE   | ✅ Yes        | ❌ No       | ✅ Yes     | ❌ No          |
| TRUNCATE | ✅ Yes        | ✅ Yes      | ❌ No      | ❌ No          |
| DROP     | ✅ Yes        | ✅ Yes      | ❌ No      | ✅ Yes         |

---

### 5. **What is the difference between `UNION` and `UNION ALL`?**

* `UNION`: Removes duplicates.
* `UNION ALL`: Keeps duplicates.

---

### 6. **Write a query to get all students with name starting with 'A'.**

```sql
SELECT * FROM students WHERE name LIKE 'A%';
```

---

### 7. **What is a Primary Key and Foreign Key?**

* **Primary Key**: Uniquely identifies each record (`student_id`)
* **Foreign Key**: Connects to a primary key in another table

---

### 8. **Write a query to find the second highest marks.**

```sql
SELECT MAX(marks)
FROM students
WHERE marks < (SELECT MAX(marks) FROM students);
```

---

### 9. **What is a subquery?**

**Answer**: A query inside another query. Example:

```sql
SELECT * FROM students 
WHERE marks > (SELECT AVG(marks) FROM students);
```

---

### 10. **What is a JOIN? Explain types.**

**Answer**:

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL JOIN
* SELF JOIN

```sql
SELECT s.name, d.dept_name
FROM students s
JOIN departments d ON s.department = d.dept_code;
```

---

### 11. **Difference between `RANK()`, `DENSE_RANK()`, and `ROW_NUMBER()`**

| Function      | Skips Rank? | Uniqueness |
| ------------- | ----------- | ---------- |
| RANK()        | ✅ Yes       | ❌          |
| DENSE\_RANK() | ❌ No        | ❌          |
| ROW\_NUMBER() | ❌ No        | ✅          |

---

### 12. **What is a view?**

**Answer**: A virtual table created from a query. Doesn't store data.

```sql
CREATE VIEW cs_students AS
SELECT * FROM students WHERE department = 'CS';
```

---

### 13. **What are indexes?**

**Answer**: Used to improve the speed of SELECT queries by allowing faster lookups.

```sql
CREATE INDEX idx_city ON students(city);
```

---

### 14. **What are aggregate functions?**

* `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`

```sql
SELECT AVG(marks) FROM students;
```

---

### 15. **Write a query to count students from each city.**

```sql
SELECT city, COUNT(*) FROM students GROUP BY city;
```

---

### 16. **What is normalization?**

**Answer**: Organizing data to reduce redundancy.

* 1NF – Remove repeating groups
* 2NF – Remove partial dependencies
* 3NF – Remove transitive dependencies

---

### 17. **What is a CTE?**

**Answer**: Common Table Expression — used to simplify complex queries.

```sql
WITH top_students AS (
  SELECT * FROM students WHERE marks > 90
)
SELECT * FROM top_students;
```

---

### 18. **What is a trigger?**

**Answer**: A block of SQL that runs automatically when an event occurs (INSERT, UPDATE, DELETE).

---

### 19. **What is a stored procedure?**

**Answer**: A precompiled set of SQL statements stored in the database.

---

### 20. **What is the difference between `IN` and `EXISTS`?**

* `IN`: Checks if a value exists in a list.
* `EXISTS`: Checks for the existence of rows in a subquery.

---

### 21. **Write a query to fetch top 2 scorers per department.**

```sql
SELECT * FROM (
  SELECT *, RANK() OVER (PARTITION BY department ORDER BY marks DESC) AS rnk
  FROM students
) ranked
WHERE rnk <= 2;
```

---

### 22. **What are ACID properties?**

* **A**tomicity: All or nothing
* **C**onsistency: Valid state
* **I**solation: Concurrent transactions don't clash
* **D**urability: Committed changes are permanent

---

### 23. **Write a query to swap two columns (age and marks).**

```sql
UPDATE students SET age = marks, marks = age;
-- Note: In real DB, use temp variable or two updates
```

---

### 24. **How to delete duplicate rows but keep one?**

```sql
DELETE FROM students
WHERE student_id NOT IN (
  SELECT MIN(student_id)
  FROM students
  GROUP BY name, age, gender, department, marks, city
);
```

---

### 25. **Write a query to find palindromes in student names.**

```sql
SELECT * FROM students
WHERE name = REVERSE(name);
```

---


