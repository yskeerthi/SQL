Perfect Keerthi! Now that your `students` table is ready, let’s walk through **all operations** — from **basic to advanced** — that you can perform using SQL on this table.

---

## 🧑‍🎓 `students` Table Structure:

| Column      | Type        |
| ----------- | ----------- |
| student\_id | INT (PK)    |
| name        | VARCHAR(50) |
| age         | INT         |
| gender      | CHAR(1)     |
| department  | VARCHAR(10) |
| marks       | INT         |
| city        | VARCHAR(50) |

---

# ✅ BASIC OPERATIONS

### 1. **View all records**

```sql
SELECT * FROM students;
```

### 2. **Select specific columns**

```sql
SELECT name, marks FROM students;
```

### 3. **Filter with WHERE**

```sql
SELECT * FROM students WHERE city = 'Hyderabad';
SELECT * FROM students WHERE marks > 85;
```

### 4. **Sort data**

```sql
SELECT * FROM students ORDER BY marks DESC;
```

### 5. **Limit output**

```sql
SELECT * FROM students LIMIT 3;
```

### 6. **DISTINCT values**

```sql
SELECT DISTINCT department FROM students;
```

---

# 🔁 CONDITIONAL OPERATORS

### 7. **IN, BETWEEN, LIKE**

```sql
SELECT * FROM students WHERE department IN ('CS', 'IT');
SELECT * FROM students WHERE marks BETWEEN 80 AND 90;
SELECT * FROM students WHERE name LIKE 'K%';  -- starts with K
```

---

# 🧮 AGGREGATE FUNCTIONS

### 8. **COUNT, SUM, AVG, MIN, MAX**

```sql
SELECT COUNT(*) FROM students;
SELECT AVG(marks) FROM students;
SELECT MAX(marks), MIN(marks) FROM students;
```

---

# 📊 GROUPING & FILTERING GROUPS

### 9. **GROUP BY**

```sql
SELECT department, AVG(marks) FROM students GROUP BY department;
```

### 10. **GROUP BY with HAVING**

```sql
SELECT city, COUNT(*) FROM students GROUP BY city HAVING COUNT(*) > 1;
```

---

# ✍️ DATA MODIFICATION

### 11. **INSERT a new student**

```sql
INSERT INTO students VALUES (106, 'Ajay', 22, 'M', 'CS', 90, 'Delhi');
```

### 12. **UPDATE a student’s marks**

```sql
UPDATE students SET marks = 99 WHERE student_id = 101;
```

### 13. **DELETE a student**

```sql
DELETE FROM students WHERE student_id = 106;
```

---

# 🧠 ADVANCED SQL

### 14. **CASE (conditional column)**

```sql
SELECT name, marks,
  CASE
    WHEN marks >= 90 THEN 'Excellent'
    WHEN marks >= 80 THEN 'Good'
    ELSE 'Average'
  END AS performance
FROM students;
```

### 15. **Subquery**

```sql
SELECT * FROM students
WHERE marks > (SELECT AVG(marks) FROM students);
```

---

# 🔗 JOIN (Using a 2nd table)

### 16. Create another table:

```sql
CREATE TABLE departments (
  dept_code VARCHAR(10),
  dept_name VARCHAR(50)
);

INSERT INTO departments VALUES
('CS', 'Computer Science'),
('ECE', 'Electronics & Communication'),
('IT', 'Information Technology');
```

### 17. **INNER JOIN**

```sql
SELECT s.name, d.dept_name
FROM students s
JOIN departments d ON s.department = d.dept_code;
```

---

# 🪟 WINDOW FUNCTIONS

### 18. **RANK students by marks (within departments)**

```sql
SELECT name, department, marks,
  RANK() OVER (PARTITION BY department ORDER BY marks DESC) AS dept_rank
FROM students;
```

---

# 🗂 VIEWS & INDEXES

### 19. **Create a view**

```sql
CREATE VIEW cs_students AS
SELECT * FROM students WHERE department = 'CS';
```

### 20. **Index (improves speed in large tables)**

```sql
CREATE INDEX idx_city ON students(city);
```

---

# 🔄 UNION & INTERSECT

### 21. **UNION**

```sql
SELECT name FROM students WHERE city = 'Hyderabad'
UNION
SELECT name FROM students WHERE department = 'CS';
```

---

# 🎯 BONUS CHALLENGE QUERIES

### 🧩 Get Top 2 students from each department

```sql
SELECT * FROM (
  SELECT *, RANK() OVER (PARTITION BY department ORDER BY marks DESC) AS rnk
  FROM students
) ranked
WHERE rnk <= 2;
```

---

## ⚡ Summary by Difficulty

| Level        | Operations                                                 |
| ------------ | ---------------------------------------------------------- |
| **Basic**    | SELECT, WHERE, ORDER BY, INSERT, UPDATE, DELETE            |
| **Medium**   | GROUP BY, HAVING, CASE, JOIN, Subqueries                   |
| **Advanced** | Window functions, Views, Indexes, RANK, CTEs, UNION, Index |

---

Would you like me to give:

* 💻 SQL tasks for each level?
* 📝 PDF of these notes?
* 🌐 A OneCompiler link with all these loaded?

Just tell me what you need next.
