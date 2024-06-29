---
title: "How to Prevent SQL Injection Vulnerabilities"
seoTitle: "Prevent SQL Injection with These Tips"
seoDescription: "Prevent SQL injection with prepared statements, stored procedures, and other defense methods for robust security"
datePublished: Sat Jun 29 2024 03:24:37 GMT+0000 (Coordinated Universal Time)
cuid: clxzk6jpl000008mjb0jp1g7a
slug: how-to-prevent-sql-injection-vulnerabilities
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719591412484/4c089eaf-1fd6-4c0c-95ed-6957f4985224.jpeg
tags: sql, pentesting, application-security, cybersecurity-1, sqlinjection, ethicalhacking

---

Now that you know what a SQL injection vulnerability is, how to find it, and how to exploit it, the next essential skill is learning how to prevent SQL injection vulnerabilities. This knowledge is crucial, especially when writing pentesting reports and providing clients with recommendations to remediate the discovered vulnerabilities.

## Primary and Additional Defenses

There are primary defenses and additional defenses that employ the concept of defense in depth. We'll discuss each defense as mentioned in the Application Hackers Handbook.

The correct way to prevent SQL injection vulnerabilities is by using prepared statements or parameterized queries instead of string concatenation within a query. All other options are partial solutions and should be used only as a last resort, understanding that they might be bypassed or incorrectly implemented, potentially causing a SQL injection in the future.

### 1\. Prepared Statements (Parameterized Queries)

#### Example of Vulnerable Code:

```java
String query = "SELECT account_balance FROM user_data WHERE username = '" + request.getParameter("customerName") + "'";
```

In this example, user input (`customerName`) is directly embedded into the SQL statement, which makes it vulnerable to SQL injection.

#### Example of Safe Code Using Prepared Statements:

```java
String customerName = request.getParameter("customerName");
String query = "SELECT account_balance FROM user_data WHERE username = ?";
PreparedStatement preparedStatement = connection.prepareStatement(query);
preparedStatement.setString(1, customerName);
ResultSet resultSet = preparedStatement.executeQuery();
```

In this code, the query structure is defined with placeholders (`?`). The `setString` method specifies the actual value, ensuring the input is treated as data and not part of the SQL code. Even if the user includes SQL characters, they will be interpreted as data.

### 2\. Stored Procedures

Stored procedures are batches of statements grouped as a logical unit and stored in a database. While they can help prevent SQL injection if implemented correctly, they must be called in a parameterized way to be safe.

#### Example:

```sql
CREATE PROCEDURE getAccountBalance (IN customerName VARCHAR(50))
BEGIN
  SELECT account_balance FROM user_data WHERE username = customerName;
END;
```

This stored procedure should be called with parameterized inputs to prevent SQL injection.

### 3\. Whitelist Input Validation

Define which values are authorized and reject everything else. This is particularly useful for parameters like table names and column names that cannot be parameterized.

#### Example:

```java
String columnName = request.getParameter("columnName");
if (!"users".equals(columnName)) {
    throw new IllegalArgumentException("Invalid column name");
}
```

Here, only the value `users` is accepted, preventing attackers from injecting unauthorized strings.

### 4\. Escape All User Input

While this is a partial solution, escaping user input can help mitigate SQL injection. This should be used as a last resort.

## Additional Defenses: Defense in Depth

The concept of defense in depth involves making it as difficult as possible for an attacker to compromise your organization by providing multiple layers of protection.

### Least Privilege

The application should use the lowest possible privileges when accessing the database. This minimizes the damage an attacker can do if they exploit a SQL injection vulnerability.

### Remove Unnecessary Default Functionality

Any unnecessary default functionality in the database should be removed or disabled, such as functions that allow executing system commands or making network connections.

### Apply Security Benchmarks

Follow benchmarks for database configuration to ensure security, including using the lowest possible privilege and removing unnecessary functionality.

### Timely Security Patches

Apply all vendor-issued security patches promptly to reduce the window of time an attacker has to exploit a known vulnerability.

### Whitelist Input Validation (Reiterated)

In addition to parameterized queries, use whitelist input validation to further protect against SQL injection by only accepting known, valid inputs.

## Conclusion

By implementing these primary and additional defenses, you can significantly reduce the risk of SQL injection vulnerabilities in your applications. Prepared statements are the most effective way to prevent SQL injection, but combining multiple layers of defense provides the best protection for your systems.