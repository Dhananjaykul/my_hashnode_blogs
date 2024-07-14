---
title: "Part 4: Advanced SQL Concepts - Joins, Subqueries, and Indexes"
seoTitle: "Advanced SQL: Joins, Subqueries, Indexes"
seoDescription: "Learn joins, subqueries, and indexes for efficient SQL data retrieval and better database performance. Enhance your querying skills"
datePublished: Sun Jul 14 2024 11:56:55 GMT+0000 (Coordinated Universal Time)
cuid: clyli35v500030aij7xccfqul
slug: part-4-advanced-sql-concepts-joins-subqueries-and-indexes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720957534217/e24e72bc-ae39-4269-bbd7-75ab554be96f.jpeg
tags: computer-science, sql

---

Welcome to the fourth part of our SQL series. In this installment, we will explore more advanced SQL concepts, including joins, subqueries, and indexes. These concepts are essential for efficient data retrieval and manipulation, allowing you to handle complex queries with ease.

### Tables and Data Setup

Before diving into the concepts, let's set up some sample tables and data that we'll use throughout this part.

#### Creating the Database and Tables

```sql
CREATE DATABASE CompanyDB;
USE CompanyDB;

CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(100),
  dept_id INT,
  salary DECIMAL(10, 2)
);

CREATE TABLE departments (
  dept_id INT PRIMARY KEY,
  dept_name VARCHAR(100)
);

CREATE TABLE projects (
  proj_id INT PRIMARY KEY,
  proj_name VARCHAR(100),
  dept_id INT
);

CREATE TABLE emp_projects (
  emp_id INT,
  proj_id INT,
  PRIMARY KEY (emp_id, proj_id),
  FOREIGN KEY (emp_id) REFERENCES employees(emp_id),
  FOREIGN KEY (proj_id) REFERENCES projects(proj_id)
);
```

#### Inserting Data into Tables

```sql
INSERT INTO employees (emp_id, emp_name, dept_id, salary) VALUES
(1, 'Alice', 101, 60000),
(2, 'Bob', 102, 55000),
(3, 'Charlie', 101, 70000),
(4, 'David', 103, 80000),
(5, 'Eve', 104, 65000);

INSERT INTO departments (dept_id, dept_name) VALUES
(101, 'HR'),
(102, 'Finance'),
(103, 'Engineering'),
(104, 'Marketing');

INSERT INTO projects (proj_id, proj_name, dept_id) VALUES
(1, 'Project A', 101),
(2, 'Project B', 102),
(3, 'Project C', 103),
(4, 'Project D', 104);

INSERT INTO emp_projects (emp_id, proj_id) VALUES
(1, 1),
(2, 2),
(3, 1),
(3, 3),
(4, 3),
(5, 4);
```

### Tables Content

#### `employees` Table

| emp\_id | emp\_name | dept\_id | salary |
| --- | --- | --- | --- |
| 1 | Alice | 101 | 60000.00 |
| 2 | Bob | 102 | 55000.00 |
| 3 | Charlie | 101 | 70000.00 |
| 4 | David | 103 | 80000.00 |
| 5 | Eve | 104 | 65000.00 |

#### `departments` Table

| dept\_id | dept\_name |
| --- | --- |
| 101 | HR |
| 102 | Finance |
| 103 | Engineering |
| 104 | Marketing |

#### `projects` Table

| proj\_id | proj\_name | dept\_id |
| --- | --- | --- |
| 1 | Project A | 101 |
| 2 | Project B | 102 |
| 3 | Project C | 103 |
| 4 | Project D | 104 |

#### `emp_projects` Table

| emp\_id | proj\_id |
| --- | --- |
| 1 | 1 |
| 2 | 2 |
| 3 | 1 |
| 3 | 3 |
| 4 | 3 |
| 5 | 4 |

### Joins

Joins are used to combine rows from two or more tables based on a related column. There are different types of joins, each serving a specific purpose.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720954960541/59d52611-d0f6-44f7-8d71-4875ecab242c.jpeg align="center")

#### Inner Join

An inner join returns only the rows that have matching values in both tables.

##### Example: List all employees with their department names

```sql
SELECT e.emp_id, e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

#### Expected Output

| emp\_id | emp\_name | dept\_name |
| --- | --- | --- |
| 1 | Alice | HR |
| 2 | Bob | Finance |
| 3 | Charlie | HR |
| 4 | David | Engineering |
| 5 | Eve | Marketing |

#### Left Join

A left join returns all rows from the left table and the matched rows from the right table. If no match is found, NULL values are returned for columns from the right table.

##### Example: List all employees and their projects, if any

```sql
SELECT e.emp_id, e.emp_name, p.proj_name
FROM employees e
LEFT JOIN emp_projects ep ON e.emp_id = ep.emp_id
LEFT JOIN projects p ON ep.proj_id = p.proj_id;
```

#### Expected Output

| emp\_id | emp\_name | proj\_name |
| --- | --- | --- |
| 1 | Alice | Project A |
| 2 | Bob | Project B |
| 3 | Charlie | Project A |
| 3 | Charlie | Project C |
| 4 | David | Project C |
| 5 | Eve | Project D |

#### Right Join

A right join returns all rows from the right table and the matched rows from the left table. If no match is found, NULL values are returned for columns from the left table.

##### Example: List all projects and their assigned employees, if any

```sql
SELECT p.proj_name, e.emp_name
FROM projects p
RIGHT JOIN emp_projects ep ON p.proj_id = ep.proj_id
RIGHT JOIN employees e ON ep.emp_id = e.emp_id;
```

#### Expected Output

| proj\_name | emp\_name |
| --- | --- |
| Project A | Alice |
| Project B | Bob |
| Project A | Charlie |
| Project C | Charlie |
| Project C | David |
| Project D | Eve |

### Subqueries

Subqueries, also known as inner queries or nested queries, are used to perform operations that require the results of one query to be used in another query. They can be placed in various parts of a SQL statement, including the `SELECT`, `FROM`, `WHERE`, and `HAVING` clauses. Here are detailed examples to illustrate the use of subqueries in different situations:

#### Example: Subquery in the SELECT Clause

A subquery in the `SELECT` clause allows you to include a value calculated by a subquery in the main query's result set.

##### Scenario: Retrieve the average salary along with each employee's details

```sql
SELECT emp_id, emp_name, salary, 
       (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;
```

#### Expected Output

| emp\_id | emp\_name | salary | avg\_salary |
| --- | --- | --- | --- |
| 1 | Alice | 60000.00 | 66000.00 |
| 2 | Bob | 55000.00 | 66000.00 |
| 3 | Charlie | 70000.00 | 66000.00 |
| 4 | David | 80000.00 | 66000.00 |
| 5 | Eve | 65000.00 | 66000.00 |

#### Example: Subquery in the FROM Clause

A subquery in the `FROM` clause, also known as an inline view, allows you to create a temporary result set that the main query can refer to.

##### Scenario: Find departments with their total salaries

```sql
SELECT d.dept_name, total_salary
FROM departments d
JOIN (
    SELECT dept_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY dept_id
) e ON d.dept_id = e.dept_id;
```

#### Expected Output

| dept\_name | total\_salary |
| --- | --- |
| HR | 130000.00 |
| Finance | 55000.00 |
| Engineering | 80000.00 |
| Marketing | 65000.00 |

#### Example: Subquery in the WHERE Clause

A subquery in the `WHERE` clause can be used to filter the results of the main query based on the result of the subquery.

##### Scenario: List employees who earn more than the average salary

```sql
SELECT emp_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

#### Expected Output

| emp\_name | salary |
| --- | --- |
| Charlie | 70000.00 |
| David | 80000.00 |

#### Example: Subquery in the HAVING Clause

A subquery in the `HAVING` clause allows you to filter groups based on the result of the subquery.

##### Scenario: Find departments with an average salary higher than 60000

```sql
SELECT dept_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > 60000;
```

#### Expected Output

| dept\_id | avg\_salary |
| --- | --- |
| 101 | 65000.00 |
| 103 | 80000.00 |

### Additional Examples

#### Example: Subquery with IN Clause

Using a subquery with the `IN` clause allows you to filter the main query's results based on a list of values returned by the subquery.

##### Scenario: Find employees who are working on 'Project A'

```sql
SELECT emp_name
FROM employees
WHERE emp_id IN (SELECT emp_id FROM emp_projects WHERE proj_id = 1);
```

#### Expected Output

| emp\_name |
| --- |
| Alice |
| Charlie |

#### Example: Correlated Subquery

A correlated subquery is a subquery that references columns from the outer query. It is executed once for each row processed by the outer query.

##### Scenario: Find employees who earn more than the average salary in their department

```sql
SELECT emp_name, salary
FROM employees e1
WHERE salary > (SELECT AVG(salary) FROM employees e2 WHERE e1.dept_id = e2.dept_id);
```

#### Expected Output

| emp\_name | salary |
| --- | --- |
| Charlie | 70000.00 |
| David | 80000.00 |

### Practice Questions

1. **Find the maximum salary in each department**
    

```sql
SELECT dept_id, MAX(salary) AS max_salary
FROM employees
GROUP BY dept_id;
```

2. **List all projects with no employees assigned**
    

```sql
SELECT proj_name
FROM projects
WHERE proj_id NOT IN (SELECT proj_id FROM emp_projects);
```

3. **Find employees who are not assigned to any project**
    

```sql
SELECT emp_name
FROM employees
WHERE emp_id NOT IN (SELECT emp_id FROM emp_projects);
```

### Indexes

Indexes are used to speed up the retrieval of data from a database table. They are particularly useful for large tables where search performance is crucial.

#### Example: Creating an Index on the `emp_name` Column

```sql
CREATE INDEX idx_emp_name ON employees(emp_name);
```

This index will improve the speed of queries that search for employees by name.

#### Example: Using Index in a Query

```sql
SELECT * FROM employees
WHERE emp_name = 'Alice';
```

### Exercises

#### Exercise 1: Find Departments with More than One Employee

1. Write a query to list department names that have more than one employee.
    

```sql

SELECT d.dept_name, COUNT(e.emp_id) AS emp_count
FROM departments d
JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_name
HAVING emp_count > 1;
```

### Expected Output

| dept\_name | emp\_count |
| --- | --- |
| HR | 2 |

#### Exercise 2: Find Projects with No Assigned Employees

1. Write a query to list project names that have no employees assigned.
    

```sql

SELECT p.proj_name
FROM projects p
LEFT JOIN emp_projects ep ON p.proj_id = ep.proj_id
WHERE ep.emp_id IS NULL;
```

### Expected Output

| proj\_name |
| --- |
| (No Output) |

#### Exercise 3: Update Department Names

Update the name of the 'HR' department to 'Human Resources'.

```sql

UPDATE departments
SET dept_name = 'Human Resources'
WHERE dept_name = 'HR';
```

### Practice Questions

Write a query to list all employees who work in the 'Engineering' department and are assigned to 'Project C'.

```sql
SELECT e.emp_name
FROM employees e
JOIN emp_projects ep ON e.emp_id = ep.emp_id
JOIN projects p ON ep.proj_id = p.proj_id
JOIN departments d ON e.dept_id = d.dept_id
WHERE d.dept_name = 'Engineering' AND p.proj_name = 'Project C';
```

Given the `employees`, `departments`, and `projects` tables, write a query to list the names of employees who are not assigned to any project.

```sql
SELECT e.emp_name


FROM employees e
LEFT JOIN emp_projects ep ON e.emp_id = ep.emp_id
WHERE ep.proj_id IS NULL;
```

By mastering these SQL concepts, you can handle more complex queries and optimize your database interactions effectively. In the next part, we will delve into SQL interview questions. Stay tuned!