---
title: "SQL Tutorial Part 2: Keys, Constraints, and Advanced Queries"
seoTitle: "SQL Tutorial Part 2: Keys and Constraints Guide"
seoDescription: "Explore SQL keys, constraints, advanced queries, and practice exercises to enhance your database management skills"
datePublished: Sat Jul 06 2024 05:27:37 GMT+0000 (Coordinated Universal Time)
cuid: cly9onpdg000609l7dvu65xtc
slug: sql-tutorial-part-2-keys-constraints-and-advanced-queries
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720240384191/0e7914df-d9db-4179-b8a4-06ab260ed46b.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720240676274/57dcc16a-5ba5-4c03-9365-bdb0b52d47fb.jpeg
tags: databases, sql, devops, cybersecurity-1

---

Welcome to the second part of our comprehensive SQL tutorial. In this section, we'll dive deeper into keys, constraints, and advanced SQL queries. We'll also include practice exercises to help solidify our understanding.

## Keys in SQL

### Primary Keys

A primary key is a column (or a set of columns) in a table that uniquely identifies each row in that table. Each table can have only one primary key, and it must not contain NULL values.

**Example:**

```sql
CREATE TABLE student (
  rollno INT PRIMARY KEY,
  name VARCHAR(50),
  marks INT NOT NULL,
  grade VARCHAR(1),
  city VARCHAR(20)
);
```

### Foreign Keys

A foreign key is a column (or a set of columns) that refers to the primary key of another table. It helps maintain referential integrity between two related tables.

**Example:**

```sql
CREATE TABLE city (
  city_id INT PRIMARY KEY,
  city_name VARCHAR(50)
);

CREATE TABLE student (
  student_id INT PRIMARY KEY,
  student_name VARCHAR(50),
  city_id INT,
  FOREIGN KEY (city_id) REFERENCES city(city_id)
);
```

## Constraints

Constraints are rules enforced on data columns to ensure the integrity and reliability of the data.

### NOT NULL

Ensures that a column cannot have a NULL value.

**Example:**

```sql
CREATE TABLE temp1 (
  id INT NOT NULL
);
```

### UNIQUE

Ensures that all values in a column are unique.

**Example:**

```sql
CREATE TABLE temp1 (
  id INT UNIQUE
);

INSERT INTO temp1 VALUES (101); -- Success
INSERT INTO temp1 VALUES (101); -- Error: Duplicate entry '101'
```

### PRIMARY KEY

Combines a UNIQUE constraint and a NOT NULL constraint, ensuring that a column (or a combination of columns) uniquely identifies each row.

**Example:**

```sql
CREATE TABLE temp1 (
  id INT PRIMARY KEY
);
```

### FOREIGN KEY

Prevents actions that would destroy links between tables.

**Example:**

```sql
CREATE TABLE temp (
  cust_id INT,
  FOREIGN KEY (cust_id) REFERENCES customer(id)
);
```

### DEFAULT

Sets a default value for a column if no value is specified.

**Example:**

```sql
CREATE TABLE emp (
  id INT,
  salary INT DEFAULT 25000
);

INSERT INTO emp (id) VALUES (101);
SELECT * FROM emp;
```

**Expected Output:**

| id | salary |
| --- | --- |
| 101 | 25000 |

### CHECK

Ensures that all values in a column satisfy a specific condition.

**Example:**

```sql
CREATE TABLE newTab (
  age INT CHECK (age >= 18)
);
```

## Creating a Database for College & Inserting Data

**Example:**

```sql
CREATE DATABASE college;
USE college;

CREATE TABLE student (
  rollno INT PRIMARY KEY,
  name VARCHAR(50),
  marks INT NOT NULL,
  grade VARCHAR(1),
  city VARCHAR(20)
);

INSERT INTO student (rollno, name, marks, grade, city)
VALUES
(101, "SHAMBHU", 78, "C", "Pune"),
(102, "RAM", 81, "B", "Delhi"),
(103, "SONU", 91, "A", "Mumbai"),
(104, "SHAM", 60, "D", "Nagpur"),
(105, "ROHIT", 99, "A", "Chennai"),
(106, "BANTI", 85, "C", "Hyderabad");
```

### Table Content for `student`

```sql
SELECT * FROM student;
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 101 | SHAMBHU | 78 | C | Pune |
| 102 | RAM | 81 | B | Delhi |
| 103 | SONU | 91 | A | Mumbai |
| 104 | SHAM | 60 | D | Nagpur |
| 105 | ROHIT | 99 | A | Chennai |
| 106 | BANTI | 85 | C | Hyderabad |

## Selecting Data

**Basic Syntax:**

```sql
SELECT col1, col2 FROM table_name;
```

**Select All Columns:**

```sql
SELECT * FROM student;
```

**Example:**

```sql
SELECT name, marks FROM student;
```

**Expected Output:**

| name | marks |
| --- | --- |
| SHAMBHU | 78 |
| RAM | 81 |
| SONU | 91 |
| SHAM | 60 |
| ROHIT | 99 |
| BANTI | 85 |

**Select Distinct Values:**

```sql
SELECT DISTINCT city FROM student;
```

**Expected Output:**

| city |
| --- |
| Pune |
| Delhi |
| Mumbai |
| Nagpur |
| Chennai |
| Hyderabad |

## WHERE Clause

The `WHERE` clause is used to filter records based on a specified condition.

**Examples:**

```sql
SELECT * FROM student WHERE marks > 80;
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 102 | RAM | 81 | B | Delhi |
| 103 | SONU | 91 | A | Mumbai |
| 105 | ROHIT | 99 | A | Chennai |
| 106 | BANTI | 85 | C | Hyderabad |

```sql
SELECT * FROM student WHERE city = "Mumbai";
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 103 | SONU | 91 | A | Mumbai |

```sql
SELECT * FROM student WHERE marks > 80 AND city = "Mumbai";
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 103 | SONU | 91 | A | Mumbai |

## Using Operators in WHERE

* **Arithmetic Operators:** +, -, \*, /, %
    
* **Comparison Operators:** =, !=, &gt;, &gt;=, &lt;, &lt;=
    
* **Logical Operators:** AND, OR, NOT, BETWEEN, LIKE, IN
    

**Examples:**

**Arithmetic and Comparison Operators:**

```sql
SELECT * FROM student WHERE marks + 10 > 100;
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 105 | ROHIT | 99 | A | Chennai |

**AND Operator:**

```sql
SELECT * FROM student WHERE marks > 90 AND city = "Mumbai";
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 103 | SONU | 91 | A | Mumbai |

**OR Operator:**

```sql
SELECT * FROM student WHERE marks > 90 OR city = "Mumbai";
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 103 | SONU | 91 | A | Mumbai |
| 105 | ROHIT | 99 | A | Chennai |

**BETWEEN Operator:**

```sql
SELECT * FROM student WHERE marks BETWEEN 80 AND 90;
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 102 | RAM | 81 | B | Delhi |
| 106 | BANTI | 85 | C | Hyderabad |

**IN Operator:**

```sql
SELECT * FROM student WHERE city IN ("Delhi", "Mumbai");
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 102 | RAM | 81 | B | Delhi |
| 103 | SONU | 91 | A | Mumbai |

**NOT Operator:**

```sql
SELECT * FROM student WHERE city NOT IN ("Delhi", "Mumbai");
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 101 | SHAMBHU | 78 | C | Pune |
| 104 | SHAM | 60 | D | Nagpur |
| 105 | ROHIT | 99 | A | Chennai |
| 106 | BANTI | 85 | C | Hyderabad |

**LIMIT Clause:**

```sql
SELECT * FROM student LIMIT 3;
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 101 | SHAMBHU | 78 | C | Pune |
| 102 | RAM | 81 | B | Delhi |
| 103 | SONU | 91 | A | Mumbai |

**ORDER BY Clause:**

```sql
SELECT * FROM student ORDER BY city ASC LIMIT 3;
```

**Expected Output:**

| rollno | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 105 | ROHIT | 99 | A | Chennai |
| 102 | RAM | 81 | B | Delhi |
| 106 | BANTI | 85 | C | Hyderabad |

## Aggregate Functions

Aggregate functions perform a calculation on a set of values and return a single value.

**Examples:**

**COUNT():**

```sql
SELECT COUNT(name) FROM student;
```

**Expected Output:**

| COUNT(name) |
| --- |
| 6 |

**MAX():**

```sql
SELECT MAX(marks) FROM student;
```

**Expected Output:**

| MAX(marks) |
| --- |
| 99 |

**MIN():**

```sql
SELECT MIN(marks) FROM student;
```

**Expected Output:**

| MIN(marks) |
| --- |
| 60 |

**SUM():**

```sql
SELECT SUM(marks) FROM student;
```

**Expected Output:**

| SUM(marks) |
| --- |
| 494 |

**AVG():**

```sql
SELECT AVG(marks) FROM student;
```

**Expected Output:**

| AVG(marks) |
| --- |
| 82.33 |

## GROUP BY Clause

The `GROUP BY` clause groups records into summary rows, often used with aggregate functions.

**Examples:**

**Count Number of Students in Each City:**

```sql
SELECT city, COUNT(name) FROM student GROUP BY city;
```

**Expected Output:**

| city | COUNT(name) |
| --- | --- |
| Pune | 1 |
| Delhi | 1 |
| Mumbai | 1 |
| Nagpur | 1 |
| Chennai | 1 |
| Hyderabad | 1 |

## Practice Exercises

### Exercise 1

Write a query to find the average marks in each city in ascending order.

<details>
<summary>Solution</summary>
<pre><code class="language-sql">SELECT city, AVG(marks) FROM student GROUP BY city ORDER BY AVG(marks);</code></pre>
<p><strong>Expected Output:</strong></p>
<table>
<thead>
<tr>
<th>city</th>
<th>AVG(marks)</th>
</tr>
</thead>
<tbody>
<tr>
<td>Nagpur</td>
<td>60</td>
</tr>
<tr>
<td>Pune</td>
<td>78</td>
</tr>
<tr>
<td>Delhi</td>
<td>81</td>
</tr>
<tr>
<td>Hyderabad</td>
<td>85</td>
</tr>
<tr>
<td>Mumbai</td>
<td>91</td>
</tr>
<tr>
<td>Chennai</td>
<td>99</td>
</tr>
</tbody>
</table>
</details>

### Exercise 2

Given a table with columns customer\_id, customers, mode of payments, city. Find the total payment according to each payment method.

<details>
<summary>Solution</summary>
<pre><code class="language-sql">SELECT mode, COUNT(customer_id) FROM payment_table GROUP BY mode;</code></pre>
</details>

### Exercise 3

Create a database named `LibraryDB`, create tables for `books` and `authors`, and insert sample data.

<details>
<summary>Solution</summary>
<pre><code class="language-sql">CREATE DATABASE LibraryDB;
USE LibraryDB;
CREATE TABLE authors (
  author_id INT PRIMARY KEY,
  author_name VARCHAR(100)
);
CREATE TABLE books (
  book_id INT PRIMARY KEY,
  title VARCHAR(100),
  author_id INT,
  FOREIGN KEY (author_id) REFERENCES authors(author_id)
);
INSERT INTO authors (author_id, author_name) VALUES (1, 'George Orwell'), (2, 'Harper Lee'), (3, 'F. Scott Fitzgerald');
INSERT INTO books (book_id, title, author_id) VALUES (1, '1984', 1), (2, 'To Kill a Mockingbird', 2), (3, 'The Great Gatsby', 3);
SELECT * FROM authors;
SELECT * FROM books;</code></pre></details>

### Expected Output for `authors` Table

| author\_id | author\_name |
| --- | --- |
| 1 | George Orwell |
| 2 | Harper Lee |
| 3 | F. Scott Fitzgerald |

### Expected Output for `books` Table

| book\_id | title | author\_id |
| --- | --- | --- |
| 1 | 1984 | 1 |
| 2 | To Kill a Mockingbird | 2 |
| 3 | The Great Gatsby | 3 |

This concludes the second part of our SQL tutorial. In the next part, we will explore more advanced SQL topics and queries. Stay tuned!