---
title: "Error Handling and Debugging in Python: A Comprehensive Guide"
seoTitle: "Error Handling and Debugging in Python: A Comprehensive Guide!"
seoDescription: "Welcome to Part 8 of our Python for Scripting series! In this segment, we'll explore the critical aspects of error handling, exception handling,& debugging."
datePublished: Fri Nov 17 2023 14:31:04 GMT+0000 (Coordinated Universal Time)
cuid: clp2pwyf0000208juhlxv5n8p
slug: error-handling-and-debugging-in-python-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700229370891/92fa3889-0fd0-45f3-bd3a-1109e0990224.gif
tags: python, error-handling, devops, cybersecurity-1, python-scripting

---

Welcome to Part 8 of our Python for Scripting series! In this segment, we'll explore the critical aspects of error handling, exception handling, and debugging techniques in Python, particularly valuable for DevOps and cybersecurity-related automation tasks.

## **Exception Handling in Python**

![Exception & Error Handling in Python for Professionals: A Comprehensive  Guide with FastAPI | by Ashok Poudel | GoPenAI](https://miro.medium.com/v2/resize:fit:1358/0*XfadqfGO8EUX1m_1.png align="left")

Python provides robust mechanisms for handling exceptions that occur during program execution. Key constructs include `try`, `except`, `else`, and `finally`.

### **Basics of Exception Handling**

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Error occurred:", e)
else:
    print("No errors detected.")
finally:
    print("Exception handling complete.")
```

**Explanation:**

* The `try` block attempts the code that might raise an exception.
    
* The `except ZeroDivisionError as e:` block catches and handles the specific `ZeroDivisionError` exception, printing the error message.
    
* The `else` block executes if no exceptions occur within the `try` block.
    
* The `finally` block always executes regardless of whether an exception occurred or not.
    

**Expected Output:**

```plaintext
Error occurred: division by zero
Exception handling complete.
```

### **Handling Real-world Scenarios**

```python
def open_file(filename):
    try:
        with open(filename, 'r') as file:
            contents = file.read()
            print("File contents:", contents)
    except FileNotFoundError as e:
        print("File not found:", e)

open_file("example.txt")
```

**Explanation:**

* The `open_file()` function attempts to open a file for reading.
    
* If the file does not exist, it raises a `FileNotFoundError`, which is caught and handled by the `except` block.
    
* In the `except` block, an appropriate error message is printed.
    

**Expected Output:**

```plaintext
File not found: [Errno 2] No such file or directory: 'example.txt'
```

## **Debugging Tools and Techniques**

![Debugging Techniques for Python Code](https://www.startertutorials.com/blog/wp-content/uploads/2023/04/Debugging-Techniques-for-Python-Code.png align="left")

Effective debugging is crucial for identifying and fixing issues in code. Python offers various debugging tools and techniques, including print statements and dedicated debugging libraries like `pdb`.

## **Utilizing Print Statements for Debugging**

Print statements are a simple yet effective method for debugging. They help display intermediate values and messages during code execution.

```python
def calculate_division(a, b):
    print(f"Dividing {a} by {b}")
    try:
        result = a / b
        print("Division result:", result)
    except ZeroDivisionError as e:
        print("Error:", e)

calculate_division(10, 2)
calculate_division(8, 0)
```

**Explanation:**

* The `calculate_division()` function attempts division and uses `print()` statements strategically to display values and messages.
    
* It prints the numbers being divided and the result.
    
* If a division by zero occurs, the `ZeroDivisionError` is caught and handled, displaying an appropriate error message.
    

**Expected Output:**

```plaintext
Dividing 10 by 2
Division result: 5.0
Dividing 8 by 0
Error: division by zero
```

## **Debugging Complex Code with** `pdb`

Python's built-in `pdb` library offers a powerful debugging environment allowing step-by-step code execution and variable inspection.

```python
import pdb

def complex_function(a, b):
    result = a * b
    pdb.set_trace()  # Start debugging session
    result += a + b
    return result

complex_function(5, 10)
```

**Explanation:**

* `pdb.set_trace()` sets a breakpoint in the code, initiating a debugging session.
    
* When the code reaches this point, it halts execution, and you can interactively inspect variables, step through code execution, and identify issues.
    
* Commands like `step`, `next`, `continue`, and `print` can be used to navigate through the code.
    

**Expected Output (Debugging Session):**

```plaintext
> ...path to file...
(Pdb) continue
```

## **Additional Debugging Techniques**

### Logging for Debugging

Using the `logging` module helps trace the flow of your program by logging messages at different severity levels.

```python
import logging

logging.basicConfig(level=logging.DEBUG)

def some_function():
    logging.debug('This is a debug message')
    # Rest of the function code
```

### **Using IDE Debuggers**

Integrated Development Environments (IDEs) like PyCharm, Visual Studio Code, etc., offer built-in debuggers allowing breakpoints, step-by-step execution, and variable inspection within the IDE environment.

### **Assertion for Debugging**

`assert` statements are helpful to test conditions that should hold true during code execution. If the condition fails, it raises an `AssertionError`, highlighting potential issues.

```python
def validate_input(value):
    assert value > 0, "Value must be positive"
    # Rest of the function code
```

These debugging techniques expand your toolkit for troubleshooting and resolving issues in Python code, essential for DevOps and cybersecurity-related automation tasks.

## **Practical Exercises**

![Python Exercises and Interesting Codes - TechNData - Tech & Data](https://www.techndata.com/wp-content/uploads/2018/07/Python-exercises.png align="left")

### Exercise 1: Handling File Not Found Error

Create a function that attempts to open a file and handles the `FileNotFoundError` exception.

**Expected Output:** *(Dependent on file existence)*

### Exercise 2: Debugging Loop Logic

Identify and fix a logical error in a loop that iterates through a list of numbers and performs a calculation.

**Expected Output:** *(Corrected results of the calculation)*

### Exercise 3: Utilizing `pdb` for Debugging

Experiment with Python's built-in `pdb` library to debug a complex function or program.

**Expected Output:** *(Interactive debugging session information)*

### Exercise 4: Handling Input Validation

Write a script that validates user input and handles possible exceptions related to incorrect input formats.

**Expected Output:** *(Appropriate messages for valid/invalid inputs)*

### Exercise 5: Custom Exception Creation

Define a custom exception class and use it to handle a specific scenario in your code.

**Expected Output:** *(Handled custom exception messages)*

Mastering error handling and debugging in Python is pivotal for DevOps and cybersecurity-related automation tasks. Practice these exercises to enhance your troubleshooting skills and streamline your automation workflows! Stay tuned for more Python scripting adventures.

## **Solutions to Regex Practical Exercises**

### Exercise 1: Phone Number Validator

```python
import re

def validate_phone_number(phone_number):
    pattern = r"\(?\d{3}\)?[-.]?\s?\d{3}[-.]?\s?\d{4}"
    if re.match(pattern, phone_number):
        return True
    return False

# Testing the function
phone_numbers = [
    "(123) 456-7890",
    "123-456-7890",
    "123.456.7890",
    "123 456 7890",
    "1234567890"
]

for number in phone_numbers:
    if validate_phone_number(number):
        print(f"{number}: Valid phone number")
    else:
        print(f"{number}: Invalid phone number")
```

**Explanation:**

* The function `validate_phone_number()` uses regex to check various phone number formats.
    
* The regex pattern `\(?...` matches optional parentheses, followed by digits and optional separators.
    

**Expected Output:**

```plaintext
(123) 456-7890: Valid phone number
123-456-7890: Valid phone number
123.456.7890: Valid phone number
123 456 7890: Valid phone number
1234567890: Invalid phone number
```

### Exercise 2: Password Strength Checker

```python
import re

def check_password_strength(password):
    pattern = r"^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$"
    if re.match(pattern, password):
        return True
    return False

# Testing the function
passwords = [
    "P@ssw0rd",
    "Weakpass",
    "StrongP@ss123!",
    "AnotherStrong#123"
]

for pwd in passwords:
    if check_password_strength(pwd):
        print(f"{pwd}: Strong password")
    else:
        print(f"{pwd}: Weak password")
```

**Explanation:**

* The function `check_password_strength()` utilizes regex to validate password strength.
    
* The regex pattern enforces criteria: minimum length (8 characters), uppercase, lowercase, digit, and special character.
    

**Expected Output:**

```plaintext
P@ssw0rd: Strong password
Weakpass: Weak password
StrongP@ss123!: Strong password
AnotherStrong#123: Strong password
```

### Exercise 3: URL Extractor

```python
import re

def extract_urls(text):
    pattern = r"(https?://\S+)"
    urls = re.findall(pattern, text)
    return urls

# Testing the function
block_of_text = "Visit my site at https://example.com or see more at http://blog.example.com"
extracted_urls = extract_urls(block_of_text)
print("Extracted URLs:", extracted_urls)
```

**Explanation:**

* The `extract_urls()` function uses regex to find URLs in a block of text.
    
* The regex pattern matches HTTP or HTTPS URLs.
    

**Expected Output:**

```plaintext
Extracted URLs: ['https://example.com', 'http://blog.example.com']
```

### Exercise 4: IP Address Finder

```python
import re

def extract_ip_addresses(text):
    pattern = r"(\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})"
    ip_addresses = re.findall(pattern, text)
    return ip_addresses

# Testing the function
text_with_ips = "Server 1: 192.168.0.1, Server 2: 10.0.0.1, Server 3: 172.16.0.1"
extracted_ips = extract_ip_addresses(text_with_ips)
print("Extracted IP Addresses:", extracted_ips)
```

**Explanation:**

* The `extract_ip_addresses()` function uses regex to identify and extract IPv4 addresses from a block of text.
    
* The regex pattern matches sequences of digits separated by periods.
    

**Expected Output:**

```plaintext
Extracted IP Addresses: ['192.168.0.1', '10.0.0.1', '172.16.0.1']
```

### Exercise 5: HTML Tag Remover

```python
import re

def remove_html_tags(html_text):
    clean_text = re.sub(r'<.*?>', '', html_text)
    return clean_text

# Testing the function
html_document = "<html><body><h1>Title</h1><p>This is a paragraph.</p></body></html>"
cleaned_text = remove_html_tags(html_document)
print("Cleaned Text:", cleaned_text)
```

**Explanation:**

* The `remove_html_tags()` function uses regex to remove HTML tags from a given HTML document.
    
* The `re.sub()` method replaces HTML tags and their content with an empty string.
    

**Expected Output:**

```plaintext
Cleaned Text: TitleThis is a paragraph.
```

These solutions demonstrate the use of regular expressions in solving practical tasks like validating phone numbers, checking password strength, extracting URLs and IP addresses, and removing HTML tags.