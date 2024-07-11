---
title: "Part 3: Advanced SQL Concepts and Commands"
seoTitle: "Advanced SQL: Techniques and Commands"
seoDescription: "Delve into advanced SQL concepts like `HAVING` clause, foreign keys, table schema alterations, and cascading operations with practical examples"
datePublished: Thu Jul 11 2024 08:51:37 GMT+0000 (Coordinated Universal Time)
cuid: clyh15b2s000o0ajm54gl8scm
slug: part-3-advanced-sql-concepts-and-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720687641548/24b6efbe-a919-4e39-b449-f4ab17883291.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720687745369/37f527c3-02a4-415e-88d0-fdc34710beb6.jpeg
tags: databases, sql, devops, cybersecurity-1

---

In this part of our SQL series, we will delve into more advanced concepts and commands, focusing on the `HAVING` clause, table-related queries, foreign keys, cascading operations, and altering table schemas. We will also go through examples and demonstrations to ensure a clear understanding of these concepts.

### Database and Tables

Let's start by creating a sample database and tables that we will use throughout this part.

#### Creating the Database and Tables

```sql
CREATE DATABASE SchoolDB;
USE SchoolDB;

CREATE TABLE student (
  student_id INT PRIMARY KEY,
  name VARCHAR(50),
  marks INT,
  grade VARCHAR(1),
  city VARCHAR(20)
);

CREATE TABLE dept (
  dept_id INT PRIMARY KEY,
  dept_name VARCHAR(50)
);

CREATE TABLE teacher (
  teacher_id INT PRIMARY KEY,
  teacher_name VARCHAR(50),
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES dept(dept_id)
);
```

#### Inserting Data into Tables

```sql
INSERT INTO student (student_id, name, marks, grade, city) VALUES
(1, 'Alice', 95, 'A', 'New York'),
(2, 'Bob', 88, 'B', 'Los Angeles'),
(3, 'Charlie', 92, 'A', 'Chicago'),
(4, 'David', 76, 'C', 'Houston'),
(5, 'Eve', 85, 'B', 'Phoenix');

INSERT INTO dept (dept_id, dept_name) VALUES
(101, 'Science'),
(102, 'Mathematics'),
(103, 'English');

INSERT INTO teacher (teacher_id, teacher_name, dept_id) VALUES
(201, 'Dr. Smith', 101),
(202, 'Prof. Johnson', 102),
(203, 'Dr. Brown', 103);
```

### Tables Content

#### `student` Table

| student\_id | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 1 | Alice | 95 | A | New York |
| 2 | Bob | 88 | B | Los Angeles |
| 3 | Charlie | 92 | A | Chicago |
| 4 | David | 76 | C | Houston |
| 5 | Eve | 85 | B | Phoenix |

#### `dept` Table

| dept\_id | dept\_name |
| --- | --- |
| 101 | Science |
| 102 | Mathematics |
| 103 | English |

#### `teacher` Table

| teacher\_id | teacher\_name | dept\_id |
| --- | --- | --- |
| 201 | Dr. Smith | 101 |
| 202 | Prof. Johnson | 102 |
| 203 | Dr. Brown | 103 |

### HAVING Clause

The `HAVING` clause is similar to the `WHERE` clause but is used to apply conditions to groups of rows created by the `GROUP BY` clause. This is particularly useful when you want to filter groups based on aggregate values.

#### Example: Count the number of students in each city where the maximum marks exceed 90

```sql
SELECT COUNT(name) AS student_count, city
FROM student
GROUP BY city
HAVING MAX(marks) > 90;
```

### Expected Output

| student\_count | city |
| --- | --- |
| 1 | New York |
| 1 | Chicago |

### General SQL Query Order

```sql
SELECT column(s)
FROM table_name
WHERE condition    -- Applies condition on rows | used before GROUP BY
GROUP BY column(s)
HAVING condition   -- Applies condition on groups | used after GROUP BY
ORDER BY column(s) ASC;
```

#### Example: Retrieve cities with students having grade "A" and maximum marks above 90

```sql
SELECT city
FROM student
WHERE grade = 'A'
GROUP BY city
HAVING MAX(marks) > 90
ORDER BY city DESC;
```

### Expected Output

| city |
| --- |
| New York |
| Chicago |

### Table Related Queries

#### Updating Rows

The `UPDATE` command is used to modify existing rows in a table. It is essential when data needs to be corrected or updated based on new information.

##### Example: Update grades from "A" to "O"

```sql
SET SQL_SAFE_UPDATES = 0;
UPDATE student
SET grade = 'O'
WHERE grade = 'A';
```

This command may require disabling SQL safe mode to prevent accidental updates.

##### Example: Update grades based on marks range

```sql
UPDATE student
SET grade = 'B'
WHERE marks BETWEEN 70 AND 80;
```

This command changes grades to "B" for students with marks between 70 and 80.

##### Example: Increase marks by 1 for all students

```sql
UPDATE student
SET marks = marks + 1;
SELECT * FROM student;
```

### Expected Output

| student\_id | name | marks | grade | city |
| --- | --- | --- | --- | --- |
| 1 | Alice | 96 | O | New York |
| 2 | Bob | 89 | B | Los Angeles |
| 3 | Charlie | 93 | O | Chicago |
| 4 | David | 77 | B | Houston |
| 5 | Eve | 86 | B | Phoenix |

#### Deleting Rows

The `DELETE` command is used to remove rows from a table. It is useful for cleaning up obsolete or incorrect data.

##### Example: Delete students with marks less than 13

```sql
DELETE FROM student
WHERE marks < 13;
SELECT * FROM student;
```

### Expected Output

No rows should be deleted as no student has marks less than 13.

### Foreign Keys

Foreign keys are used to establish a relationship between two tables. A foreign key in one table points to a primary key in another table.

#### Example: Creating tables with foreign keys

1. **Courses Table**
    

```sql
CREATE TABLE dept (
  dept_id INT PRIMARY KEY,
  dept_name VARCHAR(50)
);
```

This table holds department information.

2. **Teachers Table**
    

```sql
CREATE TABLE teacher (
  teacher_id INT PRIMARY KEY,
  teacher_name VARCHAR(50),
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES dept(dept_id)
);
```

This table holds teacher information and links each teacher to a department using a foreign key.

### Cascading Operations on Foreign Keys

Cascading operations ensure that changes in the parent table are automatically reflected in the child table.

#### Example: Creating a table with cascading foreign key constraints

```sql
CREATE TABLE teacher (
  teacher_id INT PRIMARY KEY,
  teacher_name VARCHAR(50),
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES dept(dept_id)
  ON DELETE CASCADE
  ON UPDATE CASCADE
);
```

### Demonstration: Impact of Cascading Operations

1. **Deleting a Department**
    

```sql
DELETE FROM dept
WHERE dept_id = 101;
```

* This will automatically delete all teachers associated with the department having `dept_id = 101`.
    

2. **Updating a Department**
    

```sql
UPDATE dept
SET dept_name = 'New Science'
WHERE dept_id = 101;
```

* This will automatically update the `dept_id` in the `teacher` table for all teachers associated with the department.
    

### Altering Table Schemas

The `ALTER TABLE` command is used to modify an existing table structure. It is powerful for adapting to new requirements without recreating the table.

#### Adding a Column

```sql
ALTER TABLE student
ADD COLUMN email VARCHAR(100);
```

This command adds a new column `email` to the `student` table.

#### Dropping a Column

```sql
ALTER TABLE student
DROP COLUMN email;
```

This command removes the `email` column from the `student` table.

#### Renaming a Table

```sql
ALTER TABLE student
RENAME TO pupil;
```

This command renames the `student` table to `pupil`.

#### Renaming a Column

```sql
ALTER TABLE student
CHANGE COLUMN city location VARCHAR(50);
```

This command renames the `city` column to `location` and changes its datatype to `VARCHAR(50)`.

#### Modifying a Column

```sql
ALTER TABLE student
MODIFY grade CHAR(2);
```

This command changes the datatype of the `grade` column to `CHAR(2)`.

### Exercises with Solutions

#### Exercise 1: Update Marks and Grades

1. Update the marks of all students by adding 5 to their current marks.
    
2. Change the grade of all students with marks greater than 85 to "A".
    

<details>
<summary>Solution</summary>
<pre><code class="language-sql">
UPDATE student
SET marks = marks + 5;
UPDATE student
SET grade = 'A'
WHERE marks &gt; 85;
</code></pre>
</details>

### Practice Questions

1. Write a query to find the average marks in each city in ascending order.
    

```sql
SELECT city, AVG(marks)
FROM student
GROUP BY city
ORDER BY AVG(marks);
```

2. Given a table with columns `customer_id`, `customers`, `mode_of_payments`, `city`, find the total payment according to each payment method.
    

```sql
SELECT mode_of_payments, COUNT(customer_id)
FROM payment_table
GROUP BY mode_of_payments;
```

By understanding these advanced SQL concepts, you will be able to perform more complex queries and manage your databases more efficiently. In the next part, we will cover more intricate aspects of SQL, including joins, subqueries, and indexes. Stay tuned!