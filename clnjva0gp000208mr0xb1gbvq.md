---
title: "Loops and Iteration"
seoTitle: "Python for Scripting: Part 4 - Loops and Iteration"
seoDescription: "Welcome to Part 4 of "Python for Scripting " series! In this installment, we will explore the essential concepts of loops and iteration in Python."
datePublished: Tue Oct 10 2023 05:13:52 GMT+0000 (Coordinated Universal Time)
cuid: clnjva0gp000208mr0xb1gbvq
slug: loops-and-iteration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696914202133/403fd9f4-efe3-49fe-9cda-c809aa1677e1.png
tags: python, automation, programming-tips

---

Welcome to Part 4 of the "Python for Scripting " series! In this installment, we will explore the essential concepts of loops and iteration in Python. These concepts are fundamental for automating repetitive tasks and processing collections of data efficiently. Here's what we'll cover in this blog post:

1. **for Loops**
    
    * Basic syntax
        
    * The `range()` function
        
2. **while Loops**
    
    * Basic syntax
        
    * Loop control statements (break and continue)
        
3. **Iterating Through Lists and Other Data Structures**
    
4. **List Comprehensions**
    
    * A concise way to create lists
        

## 1\. for Loops

### Basic Syntax

A `for` loop is used to iterate over a sequence (like a list, tuple, or string) or other iterable objects. The basic syntax looks like this:

```python
for item in iterable:
    # Code to be executed for each item
```

Here's an example:

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

**Output:**

```bash
apple
banana
cherry
```

### The `range()` Function

The `range()` function generates a sequence of numbers that can be used in a `for` loop. It's commonly used when you need to repeat an operation a specific number of times.

```python
for number in range(5):
    print(number)
```

**Output:**

```bash
0
1
2
3
4
```

## 2\. while Loops

### Basic Syntax

A `while` loop continues executing as long as a condition is `True`. The basic syntax is as follows:

```python
while condition:
    # Code to be executed while the condition is True
```

Here's an example:

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

**Output:**

```bash
0
1
2
3
4
```

### Loop Control Statements

* `break`: It is used to exit the loop prematurely.
    
* `continue`: It is used to skip the rest of the current iteration and continue with the next one.
    

## 3\. Iterating Through Lists and Other Data Structures

Iterating through data structures like lists, tuples, dictionaries, and sets is a common task. You can use `for` loops to process each item or key-value pair.

**Example with a list:**

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

**Example with a dictionary:**

```python
person = {"name": "Virat", "age": 30, "city": "New Delhi"}
for key, value in person.items():
    print(key, ":", value)
```

## 4\. List Comprehensions

List comprehensions provide a concise way to create lists based on existing lists or other iterable objects. They can be a powerful tool for data manipulation.

**Example: Creating a list of squares from 1 to 5 using a list comprehension:**

```python
squares = [x**2 for x in range(1, 6)]
print(squares)
```

**Output:**

```bash
[1, 4, 9, 16, 25]
```

## Exercise

Now, let's put your knowledge of loops and iteration to the test with some exercises:

**Exercise 1:** Write a Python program to calculate the factorial of a given number using a `for` loop.

**Exercise 2:** Create a list of numbers and use a `while` loop to find the sum of all the numbers in the list.

**Exercise 3:** Given a list of words, use a `for` loop to count and print the number of letters in each word.

**Exercise 4:** Write a program that takes a list of numbers and uses a list comprehension to create a new list containing only the even numbers from the original list.

Feel free to share your solutions to these exercises in the comments section below. In the next part of our series, we'll explore advanced topics in Python scripting, so stay tuned for more Python scripting !

## **Solutions to Previous Exercises (Part 3):**

### Exercise 1:

**Question:** Given a list of numbers, write a Python program to find the sum of all the numbers in the list.

**Solution:**

```python
# Define a list of numbers
numbers = [10, 20, 30, 40, 50]

# Initialize a variable to store the sum
total = 0

# Use a for loop to iterate through the list and calculate the sum
for number in numbers:
    total += number

# Print the result
print("Sum of numbers:", total)
```

**Expected Output:**

```bash
Sum of numbers: 150
```

### Exercise 2:

**Question:** Create a list of numbers and use a `while` loop to find the sum of all the numbers in the list.

**Solution:**

```python
# Define a list of numbers
numbers = [10, 20, 30, 40, 50]

# Initialize variables
total = 0
index = 0

# Use a while loop to iterate through the list and calculate the sum
while index < len(numbers):
    total += numbers[index]
    index += 1

# Print the result
print("Sum of numbers:", total)
```

**Expected Output:**

```bash
Sum of numbers: 150
```

### Exercise 3:

**Question:** Given a list of words, use a `for` loop to count and print the number of letters in each word.

**Solution:**

```python
# Define a list of words
words = ["apple", "banana", "cherry", "date"]

# Use a for loop to iterate through the list and count the letters in each word
for word in words:
    letter_count = len(word)
    print(f"The word '{word}' has {letter_count} letters.")
```

**Expected Output:**

```bash
The word 'apple' has 5 letters.
The word 'banana' has 6 letters.
The word 'cherry' has 6 letters.
The word 'date' has 4 letters.
```

### Exercise 4:

**Question:** Write a program that takes a list of numbers and uses a list comprehension to create a new list containing only the even numbers from the original list.

**Solution:**

```python
# Define a list of numbers
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Use a list comprehension to filter even numbers
even_numbers = [x for x in numbers if x % 2 == 0]

# Print the result
print("Even numbers:", even_numbers)
```

**Expected Output:**

```bash
Even numbers: [2, 4, 6, 8, 10]
```

These detailed solutions should help you understand the exercises from Part 3 and their expected outputs. Feel free to reach out if you have any further questions or need additional explanations!