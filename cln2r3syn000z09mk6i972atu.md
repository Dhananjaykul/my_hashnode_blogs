---
title: "Python Data Structures"
seoTitle: "Python for Scripting: Part 3 - Python Data Structures"
seoDescription: "Explore Python data structures, including lists, tuples, dictionaries, and sets. Also we will discuss working with sequences and collections."
datePublished: Thu Sep 28 2023 05:44:59 GMT+0000 (Coordinated Universal Time)
cuid: cln2r3syn000z09mk6i972atu
slug: python-data-structures
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695878670400/c010e8fd-0991-48c4-8748-b5282db283c8.png
tags: python, devops, cybersecurity-1, datastructure

---

In the previous installments of our "Python for Scripting" series, we explored Python's basics, including variables, data types, operators, and conditional statements. Now, it's time to delve deeper into Python's powerful data structures. In Part 3, we'll cover the following topics:

1. **Lists**
    
2. **Tuples**
    
3. **Dictionaries**
    
4. **Sets**
    
5. **Working with sequences and collections**
    

## 1\. Lists

### Lists: Creation, Indexing, Slicing, and Methods

A list is a versatile and ordered collection of items. It can contain elements of different data types.

**Creation:**

```python
fruits = ["apple", "banana", "cherry"]
```

**Indexing and Slicing:**

You can access elements in a list using index numbers. Indexing starts at 0.

```python
first_fruit = fruits[0]  # "apple"
sliced_fruits = fruits[1:3]  # ["banana", "cherry"]
```

**Common List Methods**

`append()`**:** Add an item to the end of the list.

```bash
fruits = ["apple", "banana", "cherry"]
fruits.append("date")
print(fruits)
# Output: ['apple', 'banana', 'cherry', 'date']
```

`insert()`**:** Insert an item at a specific position.

```bash
fruits = ["apple", "banana", "cherry"]
fruits.insert(1, "orange")
print(fruits)
# Output: ['apple', 'orange', 'banana', 'cherry']
```

`remove()`**:** Remove a specific item by value.

```bash
fruits = ["apple", "banana", "cherry"]
fruits.remove("banana")
print(fruits)
# Output: ['apple', 'cherry']
```

`pop()`**:** Remove an item by index.

```bash
fruits = ["apple", "banana", "cherry"]
removed_fruit = fruits.pop(1)
print("Removed fruit:", removed_fruit)
print(fruits)
# Output: Removed fruit: banana
#         ['apple', 'cherry']
```

`len()`**:** Get the length of the list.

```bash
fruits = ["apple", "banana", "cherry"]
length = len(fruits)
print("Length of the list:", length)
# Output: Length of the list: 3
```

## 2\. Tuples

### Tuples: Creation, Immutability, and Uses

Tuples are similar to lists, but they are immutable, meaning you can't change their contents after creation.

**Creation:**

```python
coordinates = (3, 4)
```

Tuples are often used to represent fixed collections of data, such as coordinates, RGB colors, or points in a game.

## 3\. Dictionaries

### Dictionaries: Key-Value Pairs and Methods

Dictionaries store data in key-value pairs. They are unordered and very efficient for quick lookups.

**Creation:**

```python
person = {
    "name": "Virat",
    "age": 33,
    "city": "Delhi"
}
```

**Accessing Values:**

```python
name = person["name"]  # "Virat"
```

**Common Dictionary Methods**

`keys()`**:** Get a list of keys.

```bash
person = {
    "name": "Virat",
    "age": 33,
    "city": "Delhi"
}
keys = person.keys()
print("Keys:", keys)
# Output: Keys: dict_keys(['name', 'age', 'city'])
```

`values()`: Get a list of values.

```bash
person = {
    "name": "Virat",
    "age": 33,
    "city": "Delhi"
}
values = person.values()
print("Values:", values)
# Output: Values: dict_values(['Virat', 33, 'Delhi'])
```

`items()`: Get a list of key-value pairs.

```bash
person = {
    "name": "Virat",
    "age": 33,
    "city": "Delhi"
}
items = person.items()
print("Items:", items)
# Output: Items: dict_items([('name', 'Virat'), ('age', 33), ('city', 'Delhi')])
```

`get()`: Safely get the value for a key.

```bash
person = {
    "name": "Virat",
    "age": 33,
    "city": "Delhi"
}
age = person.get("age")
country = person.get("country", "India")
print("Age:", age)
print("Country:", country)
# Output: Age: 33
#         Country: India
```

## 4\. Sets

### Sets: Creation, Methods, and Common Operations

Sets are unordered collections of unique elements.

**Creation:**

```python
fruits = {"apple", "banana", "cherry"}
```

**Common Set Operations**

`add()`: Add an element to the set.

```bash
colors = {"red", "green", "blue"}
colors.add("yellow")
print(colors)
# Output: {'red', 'green', 'yellow', 'blue'}
```

`remove()`: Remove an element from the set.

```bash
colors = {"red", "green", "blue"}
colors.remove("green")
print(colors)
# Output: {'red', 'blue'}
```

`union()`: Combine two sets.

```bash
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union_set = set1.union(set2)
print(union_set)
# Output: {1, 2, 3, 4, 5}
```

`intersection()`: Find elements common to two sets.

```bash
set1 = {1, 2, 3}
set2 = {3, 4, 5}
intersection_set = set1.intersection(set2)
print(intersection_set)
# Output: {3}
```

## 5\. Working with Sequences and Collections

Python provides several built-in functions and methods for working with sequences and collections like lists, tuples, dictionaries, and sets. Examples include `len()`, `sorted()`, and `max()`.

Certainly! Let's explore in more detail how to work with sequences and collections in Python using built-in functions and methods. These functions and methods are incredibly useful for performing various operations on data structures. We'll focus on some common ones:

`1. len()`: Get the Length of a Sequence or Collection

The `len()` function is used to find the length of a sequence, collection, or any iterable object. It returns the number of elements in the object.

**Example:**

```python
fruits = ["apple", "banana", "cherry"]
length = len(fruits)
print("Length of the list:", length)
# Output: Length of the list: 3
```

`2. sorted()`: Sort Elements in a Sequence

The `sorted()` function is used to sort elements in a sequence or collection in ascending order. By default, it sorts elements alphabetically for strings and numerically for numbers.

**Example:**

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
sorted_numbers = sorted(numbers)
print("Sorted numbers:", sorted_numbers)
# Output: Sorted numbers: [1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]
```

`3. max()` and `min()`: Find Maximum and Minimum Values in a Sequence

The `max()` function returns the maximum value from a sequence, while the `min()` function returns the minimum value.

**Example:**

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
maximum = max(numbers)
minimum = min(numbers)
print("Maximum:", maximum)
print("Minimum:", minimum)
# Output: Maximum: 9
#         Minimum: 1
```

`4. sum()`: Calculate the Sum of Elements in a Sequence

The `sum()` function is used to calculate the sum of all elements in a sequence or collection.

**Example:**

```python
numbers = [1, 2, 3, 4, 5]
total = sum(numbers)
print("Sum of numbers:", total)
# Output: Sum of numbers: 15
```

`5. any()` and `all()`: Check for Truthiness in Sequences

The `any()` function returns `True` if at least one element in the sequence is `True` or `true.` The `all()` function returns `True` if all elements in the sequence are `True` or `true`.

**Example:**

```python
bool_values = [True, False, True, False]
any_true = any(bool_values)
all_true = all(bool_values)
print("Any true:", any_true)
print("All true:", all_true)
# Output: Any true: True
#         All true: False
```

`6. enumerate()`: Iterate with Index and Value

The `enumerate()` function is used to loop through a sequence or collection while keeping track of the index and value of each element.

**Example:**

```python
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(f"Index {index}: {fruit}")
```

**Output:**

```bash
Index 0: apple
Index 1: banana
Index 2: cherry
```

These functions and methods are essential tools for working with sequences and collections in Python. Whether you need to find the length of a list, sort data, calculate sums, or check the truthiness of elements, Python provides built-in functions to simplify these operations.

Now, let's conclude this part with a final exercise:

## Exercise

Now that you've learned about Python data structures, let's practice:

**Exercise 1:** Create a list of your favorite movies and print them.

**Exercise 2:** Create a tuple of your personal information (name, age, city) and display it.

**Exercise 3:** Build a dictionary representing a book with keys like "title," "author," and "year," and then print the book's details.

**Exercise 4:** Create two sets with your favorite colors and a friend's favorite colors. Find the common colors between the sets and print them.

**Exercise 5:** Given a list of words, write a Python program that finds and prints the longest word(s) in the list. If there are multiple longest words, print all of them.

## Solution to Previous Exercises (Part 2):

**Exercise 1:**

```python
# Get the user's name
name = input("What's your name? ")

# Greet the user
print("Hello, " + name + "!")
```

**Exercise 2:**

```python
# Check if a number is even or odd
number = int(input("Enter a number: "))
if number % 2 == 0:
    print(number, "is even.")
else:
    print(number, "is odd.")
```

**Exercise 3:**

```python
# Convert Celsius to Fahrenheit
celsius = float(input("Enter temperature in Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print("Temperature in Fahrenheit:", fahrenheit)
```

**Exercise 4:**

```python
# Simple calculator
num1 = float(input("Enter first number: "))
operator = input("Enter operator (+, -, *, /): ")
num2 = float(input("Enter second number: "))

if operator == '+':
    result = num1 + num2
elif operator == '-':
    result = num1 - num2
elif operator == '*':
    result = num1 * num2
elif operator == '/':
    result = num1 / num2
else:
    result = "Invalid operator"

print("Result:", result)
```

In this blog post, we explored Python data structures, including lists, tuples, dictionaries, and sets. We also discussed working with sequences and collections. These concepts are fundamental to scripting and automation tasks in Python. Feel free to share your solution in the comments section below.

In the next part of our series, we'll dive into loops and iteration, so stay tuned for more Python scripting tutorials!