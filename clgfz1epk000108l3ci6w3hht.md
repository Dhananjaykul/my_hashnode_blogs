---
title: "DevOps Guide: Python Data Types and Structures Basics"
seoTitle: "DevOps Python: Data Types & Structure Essentials"
seoDescription: "DevOps Guide: Python Data Types
1. Compare Lists, Tuples, Sets
2. Access Dictionary Tool
3. Modify & Sort Cloud Providers"
datePublished: Fri Apr 14 2023 03:10:08 GMT+0000 (Coordinated Universal Time)
cuid: clgfz1epk000108l3ci6w3hht
slug: devops-guide-python-data-types-and-structures-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681439045855/23554464-507c-44fc-a905-a5491f151ed0.webp
tags: linux, python, devops, 90daysofdevops, trainwithshubham

---

### Task 1 : Give the Difference between List, Tuple and set. Do Handson and put screenshots as per your understanding.

Lists, tuples, and sets are three commonly used data structures in Python. They are similar in some ways but differ in their characteristics and usage. Here are some key differences:

1. Lists:
    

* Lists are ordered sequences of elements.
    
* They are mutable, which means that their contents can be changed after they are created.
    
* Lists are created using square brackets \[\] or by using the list() function.
    
* Lists can contain duplicate values.
    
* Lists are often used to store data that needs to be changed or manipulated.
    
    1. Tuples:
        

* Tuples are ordered sequences of elements.
    
* They are immutable, which means that their contents cannot be changed after they are created.
    
* Tuples are created using parentheses () or by using the tuple() function.
    
* Tuples can contain duplicate values.
    
* Tuples are often used to store data that should not be changed, such as coordinates or dates.
    
    3.Sets:
    

* Sets are unordered collections of unique elements.
    
* They are mutable, which means that their contents can be changed after they are created.
    
* Sets are created using curly braces {} or by using the set() function.
    
* Sets cannot contain duplicate values.
    
* Sets are often used to perform mathematical operations such as union, intersection, and difference.
    

Here are some examples of creating and using lists, tuples, and sets:

1. Lists:
    

```bash
my_list = [1, 2, 3, 4, 4]
my_list.append(5)
print(my_list)
```

Output:

```bash
[1, 2, 3, 4, 4, 5]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681439746508/56c43e1a-7b12-4121-804c-ec632e6cc050.png align="center")

1. Tuples:
    

```bash
my_tuple = (1, 2, 3, 4, 4)
print(my_tuple)
```

Output:

```bash
(1, 2, 3, 4, 4)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681439858620/5428f6fa-82a8-4e29-a093-125274f23121.png align="center")

1. Sets
    

```bash
my_set = {1, 2, 3, 4, 4}
my_set.add(5)
print(my_set)
```

Output:

```bash
{1, 2, 3, 4, 5}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681439974294/0225963c-49f8-4143-84b6-ca8b3b0fdbe9.png align="center")

As you can see, each data structure has its own unique properties and uses. It's important to choose the right one for the task at hand.

### Task 2 : Create below Dictionary and use Dictionary methods to print your favourite tool just by using the keys of the Dictionary. \`\`\` fav\_tools = { 1:"Linux", 2:"Git", 3:"Docker", 4:"Kubernetes", 5:"Terraform", 6:"Ansible", 7:"Chef" } \`\`\`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681440446467/e899c81e-e5dd-4b66-ad43-6e3cecba61f9.png align="center")

In the above code, we created the `fav_tools` dictionary with 7 key-value pairs where the key represents a number and the value represents a tool name. We then printed our favorite tool "Linux" by using its key 1 with the dictionary's indexing operator `[].`

### Task 3 : Create a List of cloud service providers . eg. cloud\_providers = \["AWS","GCP","Azure"\] .Write a program to add `Digital Ocean` to the list of cloud\_providers and sort the list in alphabetical order.

\[Hint: Use keys to built in functions for Lists\]

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681440925751/e54e11ba-27ee-4cfb-8ece-ad4b8da8915a.png align="center")

In the above code, we created the `cloud_providers` list with 3 cloud service providers. We then used the `append()` method to add "Digital Ocean" to the list, and the `sort()` method to sort the list in alphabetical order. Finally, we printed the sorted list using the `print()` function.

Conclusion : This article provided a basic understanding of Python data types and structures, specifically lists, tuples, sets, and dictionaries. It also included hands-on tasks to help readers practice and reinforce their understanding of these concepts. By choosing the appropriate data structure for a given task, Python developers can write more efficient and effective code.