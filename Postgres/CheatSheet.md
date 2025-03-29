# 🚀 PostgreSQL Cheat Sheet

## 1️⃣ Basic Commands
```sql
-- Connect to a database
\c database_name

-- List all databases
\l

-- List all tables in the current database
\dt

-- Describe a table structure
\d table_name

-- Exit psql
\q
```

## 2️⃣ Creating & Managing Databases
```sql
-- Create a database
CREATE DATABASE mydb;

-- Drop a database
DROP DATABASE mydb;
```

## 3️⃣ Table Operations
```sql
-- Create a table
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(50)
);

-- Drop a table
DROP TABLE employees;

-- Alter a table (add a column)
ALTER TABLE employees ADD COLUMN salary DECIMAL(10,2);
```

## 4️⃣ Insert, Update & Delete Data
```sql
-- Insert data
INSERT INTO employees (name, age, department, salary)
VALUES ('Alice', 30, 'IT', 75000.00);

-- Update data
UPDATE employees
SET salary = 80000
WHERE name = 'Alice';

-- Delete data
DELETE FROM employees WHERE name = 'Alice';
```

## 5️⃣ Querying Data
```sql
-- Select all rows
SELECT * FROM employees;

-- Select specific columns
SELECT name, salary FROM employees;

-- Filter data
SELECT * FROM employees WHERE age > 25;

-- Sorting results
SELECT * FROM employees ORDER BY salary DESC;

-- Limit & Offset
SELECT * FROM employees LIMIT 5 OFFSET 10;
```

## 6️⃣ Joins
```sql
-- Inner Join
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department = d.id;

-- Left Join
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department = d.id;

-- Right Join
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department = d.id;
```

## 7️⃣ Aggregation & Grouping
```sql
-- Count employees by department
SELECT department, COUNT(*) FROM employees GROUP BY department;

-- Average salary by department
SELECT department, AVG(salary) FROM employees GROUP BY department;

-- Minimum & Maximum salary
SELECT MIN(salary), MAX(salary) FROM employees;
```

## 8️⃣ Indexing for Performance
```sql
-- Create an index
CREATE INDEX idx_employee_name ON employees(name);

-- Drop an index
DROP INDEX idx_employee_name;
```

## 9️⃣ Transactions
```sql
BEGIN;  -- Start a transaction

UPDATE employees SET salary = salary * 1.1 WHERE department = 'IT';

ROLLBACK;  -- Undo changes
-- or
COMMIT;  -- Save changes
```

## 🔟 JSON Support
```sql
-- Create a table with JSONB column
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    data JSONB
);

-- Insert JSON data
INSERT INTO products (data) VALUES ('{"name": "Laptop", "price": 1200, "brand": "Dell"}');

-- Query JSON data
SELECT data->>'name' AS product_name FROM products;
```

## 1️⃣1️⃣ Common Table Expressions (CTEs)
```sql
WITH department_avg AS (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT * FROM department_avg WHERE avg_salary > 60000;
```

## 1️⃣2️⃣ Window Functions
```sql
-- Rank employees by salary within their department
SELECT name, department, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees;
```

## 🎯 Practice Exercises
1️⃣ **Basic Queries**:
   - Retrieve all employees older than 25.
   - Find the highest-paid employee.

2️⃣ **Joins & Aggregations**:
   - Show the number of employees per department.
   - Retrieve employee names along with their department names.

3️⃣ **Transactions & Performance**:
   - Create an index on a frequently searched column.
   - Use `EXPLAIN ANALYZE` to optimize a query.
