---
title: "SQL Tutorial Part 1: Introduction to SQL Databases and Basic Operations"
seoTitle: "Introduction to SQL Databases & Basic Operations"
seoDescription: "Introduction to SQL databases, basic operations, and essential commands for beginners. Hands-on exercises to create and manipulate tables"
datePublished: Fri Jul 05 2024 09:29:44 GMT+0000 (Coordinated Universal Time)
cuid: cly8hv7j300070al60zov8h7k
slug: sql-tutorial-part-1-introduction-to-sql-databases-and-basic-operations
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720171696342/74f7b9f8-bade-4ed2-943d-4aafd96d2b10.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720171673103/2a03c049-38c6-4b11-bd1e-1a60604f7189.png
tags: databases, developer, cloud-computing, sql, devops, cybersecurity-1

---

Welcome to the first part of this comprehensive SQL tutorial. This tutorial is for beginners who want to brush up on their SQL skills and get hands-on experience with SQL commands.

## Understanding SQL Databases

A database is a structured collection of data stored and accessed electronically. In SQL, a database can have multiple tables, each storing inter-related data. For instance, in a school database, you might have tables for student marks, student fees, student subjects, etc.

### Creating an SQL Database

To create a new database, use the following command:

```sql
CREATE DATABASE student;
```

### Deleting a Database

If you need to delete a database, use the `DROP DATABASE` command:

```sql
DROP DATABASE student;
```

### Using a Database

Before working on a database, you need to select it:

```sql
USE student;
```

### Creating a Table

To create a table within a database, use the `CREATE TABLE` command. Here’s an example:

```sql
CREATE TABLE student (
  id INT PRIMARY KEY, 
  name VARCHAR(50),
  age INT NOT NULL
);
```

In this example, we used different data types:

* `INT`: Stores integer values.
    
* `VARCHAR(50)`: Stores variable-length strings up to 50 characters.
    
* `NOT NULL`: Ensures that the column cannot have a NULL value.
    

### Inserting Data into a Table

To insert data into the table, use the `INSERT INTO` command:

```sql
INSERT INTO student VALUES(1, "RAJ", 24);
INSERT INTO student VALUES(2, "RAM", 27);
INSERT INTO student VALUES(3, "SHAM", 25);
```

### Selecting Data from a Table

To view the data in the table, use the `SELECT` command:

```sql
SELECT * FROM student;
```

This command selects all columns from the `student` table.

## Overview of SQL Data Types

Understanding data types is crucial in SQL. Here are some common data types:

1. `CHAR` and `VARCHAR`: Store strings.
    
2. `BLOB`: Stores large binary objects.
    
3. `INT`: Stores integers.
    
4. `TINYINT`: Stores small integers.
    
5. `BIT`: Stores bit values.
    
6. `FLOAT` and `DOUBLE`: Store floating-point numbers.
    
7. `BOOLEAN`: Stores Boolean values.
    
8. `DATE`: Stores dates in the format `YYYY-MM-DD`.
    

### Signed vs. Unsigned

* `TINYINT UNSIGNED` (0 to 255)
    
* `TINYINT` (-128 to 127)
    

## Types of SQL Commands

1. **DDL (Data Definition Language)**: `CREATE`, `ALTER`, `RENAME`, `TRUNCATE`, `DROP`
    
2. **DQL (Data Query Language)**: `SELECT`
    
3. **DML (Data Manipulation Language)**: `INSERT`, `UPDATE`, `DELETE`
    
4. **DCL (Data Control Language)**: `GRANT`, `REVOKE`
    
5. **TCL (Transaction Control Language)**: `START TRANSACTION`, `COMMIT`, `ROLLBACK`
    

## Database Related Queries

* Create a database:
    
    ```sql
    CREATE DATABASE db_name;
    CREATE DATABASE IF NOT EXISTS db_name;
    ```
    
* Drop a database:
    
    ```sql
    DROP DATABASE db_name;
    DROP DATABASE IF EXISTS db_name;
    ```
    
* Show databases and tables:
    
    ```sql
    SHOW DATABASES;
    SHOW TABLES;
    ```
    
* Use a database:
    
    ```sql
    USE database;
    ```
    

## Table Related Queries

* Create a table:
    
    ```sql
    CREATE TABLE table_name(
      column_name1 datatype constraint,
      column_name2 datatype constraint,
    );
    ```
    
    Example:
    
    ```sql
    CREATE TABLE student (
      id INT PRIMARY KEY, 
      name VARCHAR(50),
      age INT NOT NULL
    );
    ```
    
* Drop a table:
    
    ```sql
    DROP TABLE student;
    ```
    
* Select and view all columns:
    
    ```sql
    SELECT * FROM table_name;
    ```
    
* Insert data into columns:
    
    ```sql
    INSERT INTO table_name
    (colname1, colname2)
    VALUES
    (col1_val1, col2_val2), (col1_val2, col2_val2);
    ```
    
    Example:
    
    ```sql
    INSERT INTO student
    (id, name)
    VALUES
    (101, "karan"),
    (102, "Arjun");
    ```
    

## Practice Exercises

### Exercise 1

Create a database for your company named `XYZ`, and perform the following operations:

1. Create a table inside the database to store employee info (id, name, salary).
    
2. Add the following info to the database:
    
    * 1, "adam", 25000
        
    * 2, "bob", 30000
        
    * 3, "casey", 40000
        
3. Select and view all your table data.
    

<details>
<summary>Solution</summary>
<pre><code class="language-sql">CREATE DATABASE XYZ_db;
USE XYZ_db;
CREATE TABLE employee_info(
  id INT PRIMARY KEY,
  name VARCHAR(50),
  salary INT
);

INSERT INTO employee_info
(id, name, salary)
VALUES
(1, "adam", 25000),
(2, "bob", 30000),
(3, "casey", 40000);

SELECT * FROM employee_info;</code></pre>
</details>

### Exercise 2

Create a database for a library system named `LibraryDB`, and perform the following operations:

1. Create a table inside the database to store book info (book\_id, title, author, year\_published).
    
2. Add the following info to the database:
    
    * 1, "1984", "George Orwell", 1949
        
    * 2, "To Kill a Mockingbird", "Harper Lee", 1960
        
    * 3, "The Great Gatsby", "F. Scott Fitzgerald", 1925
        
3. Select and view all your table data.
    

<details>
<summary>Solution</summary>
<pre><code class="language-sql">CREATE DATABASE LibraryDB;
USE LibraryDB;
CREATE TABLE books(
  book_id INT PRIMARY KEY,
  title VARCHAR(100),
  author VARCHAR(100),
  year_published INT
);

INSERT INTO books
(book_id, title, author, year_published)
VALUES
(1, "1984", "George Orwell", 1949),
(2, "To Kill a Mockingbird", "Harper Lee", 1960),
(3, "The Great Gatsby", "F. Scott Fitzgerald", 1925);

SELECT * FROM books;</code></pre>
</details>

### Exercise 3

Create a database for a school system named `SchoolDB`, and perform the following operations:

1. Create a table inside the database to store student info (student\_id, first\_name, last\_name, date\_of\_birth).
    
2. Add the following info to the database:
    
    * 1, "John", "Doe", "2005-05-15"
        
    * 2, "Jane", "Smith", "2006-08-22"
        
    * 3, "Jim", "Brown", "2004-12-01"
        
3. Select and view all your table data.
    

<details>
<summary>Solution</summary>
<pre><code class="language-sql">CREATE DATABASE SchoolDB;
USE SchoolDB;
CREATE TABLE students(
  student_id INT PRIMARY KEY,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  date_of_birth DATE
);

INSERT INTO students
(student_id, first_name, last_name, date_of_birth)
VALUES
(1, "John", "Doe", "2005-05-15"),
(2, "Jane", "Smith", "2006-08-22"),
(3, "Jim", "Brown", "2004-12-01");

SELECT * FROM students;</code></pre>
</details>

This concludes the first part of our SQL tutorial. In the next part, we will delve deeper into more advanced SQL commands and operations. Stay tuned!