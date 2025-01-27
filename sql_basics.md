To quickly brush up on **SQL**, here’s a concise but complete roadmap covering key topics:

---

### **1. Basics of SQL**
- **What is SQL?**
  - Structured Query Language for managing relational databases.
- **SQL Syntax:**
  - Keywords like `SELECT`, `FROM`, `WHERE`, `INSERT`, `UPDATE`, `DELETE`.

---

### **2. DDL (Data Definition Language)**
- **Commands:**
  - `CREATE`: Create tables or databases.
  - `ALTER`: Modify structure (e.g., add/drop a column).
  - `DROP`: Delete tables or databases.
  - `TRUNCATE`: Empty a table (faster than `DELETE`).
- **Example:**
  ```sql
  CREATE TABLE Employees (
      ID INT PRIMARY KEY,
      Name VARCHAR(50),
      Salary FLOAT
  );
  ALTER TABLE Employees ADD Department VARCHAR(50);
  DROP TABLE Employees;
  ```

---

### **3. DML (Data Manipulation Language)**
- **Commands:**
  - `INSERT`: Add data to tables.
  - `UPDATE`: Modify existing records.
  - `DELETE`: Remove specific records.
- **Example:**
  ```sql
  INSERT INTO Employees (ID, Name, Salary) VALUES (1, 'John', 50000);
  UPDATE Employees SET Salary = 55000 WHERE Name = 'John';
  DELETE FROM Employees WHERE ID = 1;
  ```

---

### **4. DQL (Data Query Language)**
- **Commands:**
  - `SELECT`: Retrieve data.
  - `WHERE`: Filter records.
  - `ORDER BY`: Sort data (`ASC`, `DESC`).
  - `LIMIT`: Restrict results.
  - `DISTINCT`: Remove duplicates.
- **Example:**
  ```sql
  SELECT DISTINCT Department FROM Employees;
  SELECT * FROM Employees WHERE Salary > 40000 ORDER BY Salary DESC LIMIT 5;
  ```

---

### **5. Constraints**
- **Common Constraints:**
  - `PRIMARY KEY`: Unique identifier.
  - `FOREIGN KEY`: Link tables.
  - `NOT NULL`: Disallows null values.
  - `UNIQUE`: Ensures all values in a column are unique.
  - `DEFAULT`: Assigns a default value.
  - `CHECK`: Validates conditions.
- **Example:**
  ```sql
  CREATE TABLE Orders (
      OrderID INT PRIMARY KEY,
      CustomerID INT,
      Amount FLOAT CHECK (Amount > 0),
      FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
  );
  ```

---

### **6. Joins**
- **Types:**
  - **INNER JOIN**: Only matching rows in both tables.
  - **LEFT JOIN**: All rows from the left table + matching ones from the right.
  - **RIGHT JOIN**: All rows from the right table + matching ones from the left.
  - **FULL OUTER JOIN**: All rows from both tables.
- **Example:**
  ```sql
  SELECT E.Name, D.DepartmentName
  FROM Employees E
  INNER JOIN Departments D
  ON E.DepartmentID = D.ID;
  ```

---

### **7. Aggregations**
- **Functions:**
  - `COUNT()`: Number of records.
  - `SUM()`: Total value.
  - `AVG()`: Average value.
  - `MAX()` / `MIN()`: Maximum/Minimum values.
- **Example:**
  ```sql
  SELECT Department, COUNT(*) AS EmployeeCount, AVG(Salary) AS AvgSalary
  FROM Employees
  GROUP BY Department
  HAVING AVG(Salary) > 40000;
  ```

---

### **8. Subqueries**
- **What Are Subqueries?**
  - Nested queries inside `SELECT`, `WHERE`, or `FROM`.
- **Example:**
  ```sql
  SELECT Name
  FROM Employees
  WHERE Salary > (SELECT AVG(Salary) FROM Employees);
  ```

---

### **9. Indexing**
- **Why Use Indexes?**
  - Speed up searches but slow down inserts/updates.
- **Commands:**
  ```sql
  CREATE INDEX idx_salary ON Employees(Salary);
  DROP INDEX idx_salary;
  ```

---

### **10. Transactions**
- **Key Commands:**
  - `BEGIN TRANSACTION`: Start a transaction.
  - `COMMIT`: Save changes.
  - `ROLLBACK`: Undo changes.
- **ACID Properties:**
  - Atomicity, Consistency, Isolation, Durability.
- **Example:**
  ```sql
  BEGIN TRANSACTION;
  UPDATE Employees SET Salary = 60000 WHERE ID = 1;
  ROLLBACK; -- Undo changes
  ```

---

### **11. Advanced Concepts**
- **Views:**
  - Virtual table from a query.
  ```sql
  CREATE VIEW HighEarners AS 
  SELECT * FROM Employees WHERE Salary > 50000;
  ```
- **Stored Procedures:**
  - Predefined SQL queries stored on the server.
  ```sql
  CREATE PROCEDURE GetHighEarners()
  BEGIN
      SELECT * FROM Employees WHERE Salary > 50000;
  END;
  ```
- **Triggers:**
  - Automatic execution after certain actions.
  ```sql
  CREATE TRIGGER BeforeInsert
  BEFORE INSERT ON Employees
  FOR EACH ROW
  SET NEW.Salary = IF(NEW.Salary < 30000, 30000, NEW.Salary);
  ```

---

### **12. Practice Scenarios**
- Write queries for:
  - Retrieving the top 5 highest-paid employees.
  - Joining tables like Employees and Departments.
  - Counting records in a specific department.
  - Creating a backup or restoring databases.

---

Here are the queries and explanations for each task:

---

### **1. Retrieving the Top 5 Highest-Paid Employees**
To find the top 5 employees with the highest salaries:
```sql
SELECT * 
FROM Employees
ORDER BY Salary DESC
LIMIT 5;
```

**Explanation:**
- `ORDER BY Salary DESC`: Sorts employees in descending order of their salary.
- `LIMIT 5`: Retrieves only the top 5 records.

**Example Output:**
| ID  | Name   | Salary  | DepartmentID |
|-----|--------|---------|--------------|
| 2   | Alice  | 60000   | 1            |
| 3   | Bob    | 55000   | 2            |
| 1   | John   | 50000   | 1            |

---

### **2. Joining Tables (Employees and Departments)**
If you have two tables, `Employees` and `Departments`, and want to display employee names along with their department names:

**Schema:**
- `Employees`: ID, Name, Salary, DepartmentID
- `Departments`: ID, DepartmentName

**Query:**
```sql
SELECT E.Name AS EmployeeName, D.DepartmentName 
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID = D.ID;
```

**Explanation:**
- `INNER JOIN`: Matches records from both tables where `Employees.DepartmentID = Departments.ID`.
- `E.Name` and `D.DepartmentName`: Selects the employee name and corresponding department name.

**Example Output:**
| EmployeeName | DepartmentName |
|--------------|----------------|
| Alice        | IT             |
| Bob          | HR             |
| John         | Finance        |

---

### **3. Counting Records in a Specific Department**
To count how many employees work in a specific department, say "IT":

**Query:**
```sql
SELECT COUNT(*) AS EmployeeCount
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID = D.ID
WHERE D.DepartmentName = 'IT';
```

**Explanation:**
- Joins `Employees` and `Departments` to ensure department names can be referenced.
- Filters for the `IT` department using `WHERE D.DepartmentName = 'IT'`.
- `COUNT(*)`: Counts the total number of matching employees.

**Example Output:**
| EmployeeCount |
|---------------|
| 2             |

---

### **4. Creating a Backup or Restoring Databases**
Creating and restoring a database backup depends on the SQL database management system (e.g., MySQL, PostgreSQL). Here’s how to do it in MySQL:

#### **Creating a Backup**
To create a backup of a database (e.g., `CompanyDB`):
```bash
mysqldump -u [username] -p CompanyDB > CompanyDB_backup.sql
```

**Explanation:**
- `mysqldump`: Command-line tool to create backups.
- `-u [username]`: Your MySQL username.
- `-p`: Prompts for your password.
- `CompanyDB > CompanyDB_backup.sql`: Dumps the database to a file.

---

#### **Restoring a Database**
To restore the database from the backup file:
```bash
mysql -u [username] -p CompanyDB < CompanyDB_backup.sql
```

**Explanation:**
- `mysql`: Command-line tool for database interaction.
- `CompanyDB < CompanyDB_backup.sql`: Restores the database from the backup file.

---


