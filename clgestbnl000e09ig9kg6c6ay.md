---
title: "Data Types in Python"
seoTitle: "Understanding Python Data Types"
seoDescription: "Learn about the different data types in Python, including numeric, string, boolean, list, tuple, set, and dictionary data types."
datePublished: Thu Apr 13 2023 07:28:07 GMT+0000 (Coordinated Universal Time)
cuid: clgestbnl000e09ig9kg6c6ay
slug: data-types-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681371122451/dfecc5de-03dc-4400-a848-8ccbb2bc01e2.webp
tags: linux, python, devops, 90daysofdevops, trainwithshubham

---

Python is a dynamically typed programming language, which means that the data type of a variable is determined at runtime, rather than at compile-time. Python supports a wide range of data types that can be used to represent different kinds of data. In this blog post, we will explore the various data types in Python and how to use them.

1. Numeric Data Types
    

Python has three numeric data types – int, float, and complex. Integers are whole numbers, positive or negative, without decimals. Floats are decimal numbers, while complex numbers are represented as a sum of a real part and an imaginary part.

Here's an example of how to declare and use these data types in Python:

```bash
x = 5      # int
y = 3.14   # float
z = 2 + 3j # complex

print(x)
print(y)
print(z)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681370265384/5858c1ce-cc56-4f45-b2d6-7e0f5b08b980.png align="center")

1. String Data Type
    

Strings are used to represent text data in Python. They are declared using single quotes or double quotes.

Here's an example of how to declare and use a string in Python:

```bash
name = 'Dhananjay'

print(name)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681370464312/73a4f2c6-acb0-4e31-b207-cc2e97cda543.png align="center")

1. Boolean Data Type
    

Boolean data types are used to represent true or false values. In Python, the keywords True and False are used to represent these values.

Here's an example of how to declare and use a boolean in Python:

```bash
x = True
y = False

print(x)
print(y)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681370601082/47a64110-5a62-4179-9066-f2aeb1adb307.png align="center")

1. List Data Type
    

Lists are used to store collections of items in Python. They are declared using square brackets and can contain any combination of data types.

Here's an example of how to declare and use a list in Python:

```bash
fruits = ['apple', 'banana', 'cherry']

print(fruits)
print(fruits[1]) # Accessing an element in the list
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681370680114/0574c89c-8adc-4409-9b94-cdd7babb1eee.png align="center")

1. Tuple Data Type
    

Tuples are similar to lists but are immutable, meaning that their contents cannot be changed after they are created. They are declared using parentheses.

Here's an example of how to declare and use a tuple in Python:

```bash
fruits = ('apple', 'banana', 'cherry')

print(fruits)
print(fruits[1]) # Accessing an element in the tuple
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681370819915/3479831d-2fba-4483-bea0-b2a659a859c7.png align="center")

1. Set Data Type
    

Sets are used to store collections of unique items in Python. They are declared using curly braces.

Here's an example of how to declare and use a set in Python:

```bash
fruits = {'apple', 'banana', 'cherry'}

print(fruits)
```

Output:

```bash
{'apple', 'banana', 'cherry'}
```

1. Dictionary Data Type
    

Dictionaries are used to store key-value pairs in Python. They are declared using curly braces and colons to separate the keys and values.

Here's an example of how to declare and use a dictionary in Python:

```bash
person = {
    'name': 'John Doe',
    'age': 30,
    'location': 'New York'
}

print(person)
print(person['name']) # Accessing a value using its key
```

Output:

```bash
{'name': 'John Doe', 'age': 30, 'location': 'New York'}
John Doe
```

In conclusion, Python has a rich set of data types that can be used to represent different kinds of data.