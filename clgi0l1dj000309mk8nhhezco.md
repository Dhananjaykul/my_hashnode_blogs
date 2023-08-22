---
title: "Python Libraries for DevOps"
seoTitle: "Top Python Libraries for DevOps"
seoDescription: "Optimize DevOps Python Libraries: JSON & YAML
Discover key libraries such as json, ijson, PyYAML, and ruamel.yaml for DevOps engineers handling JSON a..."
datePublished: Sat Apr 15 2023 13:28:56 GMT+0000 (Coordinated Universal Time)
cuid: clgi0l1dj000309mk8nhhezco
slug: python-libraries-for-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681565217786/6b7f8687-1234-455a-a552-af11075b56fc.webp
tags: linux, python, devops, 90daysofdevops, trainwithshubham

---

As a DevOps engineer, one of the core skills is the ability to work with various data formats, such as JSON and YAML. Fortunately, Python has many libraries that make it easy to parse and work with these formats. In this blog, we will look at some of the most popular Python libraries for working with JSON and YAML.

### **JSON in Python**

JSON (JavaScript Object Notation) is a lightweight data format that is easy to read and write for humans and easy to parse and generate for machines. JSON is widely used in modern web development, and as a DevOps engineer, you will often need to work with JSON data.

#### The json Library

Python's built-in json library provides a simple way to work with JSON data. The library has two main methods: `load()` and `dump()`. The `load()` method converts a JSON string into a Python object, and the `dump()` method converts a Python object into a JSON string.

```bash
import json

# Convert JSON string to Python object
data = '{"name": "John", "age": 30, "city": "New York"}'
person = json.loads(data)

# Convert Python object to JSON string
person['age'] = 31
data = json.dumps(person)
```

The json library is fast and efficient, making it an excellent choice for working with small to medium-sized JSON files. However, for large JSON files, it may not be the best option, as it loads the entire file into memory.

#### The ijson Library

For working with large JSON files, the ijson library can be a better choice. ijson is a Python library that allows you to iteratively parse large JSON files, which means it doesn't need to load the entire file into memory.

```bash
import ijson

# Open a large JSON file and iterate over its elements
with open('large_file.json') as f:
    parser = ijson.parse(f)
    for prefix, event, value in parser:
        if prefix == 'name' and event == 'string':
            print(value)
```

The ijson library is efficient and can handle very large JSON files, but it can be a bit more complex to use than the json library.

### **YAML in Python**

YAML (YAML Ain't Markup Language) is a human-readable data serialization format that is often used in configuration files. As a DevOps engineer, you will frequently work with YAML files to configure servers, applications, and infrastructure.

#### The PyYAML Library

The PyYAML library is a popular choice for working with YAML files in Python. The library provides two methods: `load()` and `dump()`. The `load()` method converts a YAML string into a Python object, and the `dump()` method converts a Python object into a YAML string.

```bash
import yaml

# Convert YAML string to Python object
data = '''
name: John
age: 30
city: New York
'''
person = yaml.load(data, Loader=yaml.Loader)

# Convert Python object to YAML string
person['age'] = 31
data = yaml.dump(person)
```

The PyYAML library is easy to use and efficient for small to medium-sized YAML files. However, like the json library, it loads the entire file into memory, which can be a problem for large files.

#### The ruamel.yaml Library

For working with large YAML files, the ruamel.yaml library can be a better choice. It provides similar functionality to PyYAML but can handle larger files more efficiently.

```bash
import ruamel.yaml

# Open a large YAML file and iterate over its elements
with open('large_file.yaml') as f:
    data = ruamel.yaml.load(f, ruamel.yaml
```

### Task 1 : Create a Dictionary in Python and write it to a json File.

Here's an example of how to create a dictionary in Python and write it to a JSON file:

```bash
import json

# Create a dictionary
person = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

# Write the dictionary to a JSON file
with open("person.json", "w") as f:
    json.dump(person, f)
```

In this example, we first create a dictionary called `person` with three key-value pairs: `"name"`, `"age"`, and `"city"`. We then use the `json.dump()` function to write the dictionary to a file called `person.json`.

The `json.dump()` function takes two arguments: the dictionary to be written, and the file object to which it should be written. The second argument should be opened in write mode with the `"w"` flag.

After running this code, you should see a new file called `person.json` in the current working directory. The contents of this file should look like this:

```bash
{"name": "John", "age": 30, "city": "New York"}
```

Note that the JSON data is written as a single line with no indentation. If you want to make the output more human-readable, you can pass an additional argument to `json.dump()` called `indent`, which specifies the number of spaces to use for indentation. For example:

```bash
json.dump(person, f, indent=4)
```

This would write the JSON data with a four-space indentation:

```bash
{
    "name": "John",
    "age": 30,
    "city": "New York"
}
```

### 2\. Read a json file `services.json` kept in this folder and print the service names of every cloud service provider.

### output

### aws : ec2 azure : VM gcp : compute engine

here's an example of how to read a JSON file in Python and print the service names of every cloud service provider:

```bash
import json

# Read the JSON file
with open("services.json", "r") as f:
    data = json.load(f)

# Extract the service names for each provider
for provider, services in data.items():
    print(f"{provider}: {services['service']}")
```

In this example, we first open the file `services.json` in read mode and use the `json.load()` function to load its contents into a Python object called `data`.

The `data` object is a dictionary where each key represents a cloud service provider, and the corresponding value is another dictionary containing information about their services. To extract the service name for each provider, we iterate over the key-value pairs in `data` using a for loop.

For each provider, we print the provider's name followed by the value associated with the key `"service"` in their corresponding dictionary. This should produce output that looks like this:

```bash
aws: ec2
azure: VM
gcp: compute engine
```

Note that the exact output may vary depending on the contents of the `services.json` file.

### 3\. Read YAML file using python, file `services.yaml` and read the contents to convert yaml to json

here's an example of how to read a YAML file in Python, and then convert it to JSON:

```bash
import yaml
import json

# Read the YAML file
with open("services.yaml", "r") as f:
    data = yaml.safe_load(f)

# Convert YAML to JSON
json_data = json.dumps(data)

# Print the JSON data
print(json_data)
```

In this example, we first open the file `services.yaml` in read mode and use the [`yaml.safe`](http://yaml.safe)`_load()` function to load its contents into a Python object called `data`.

The `data` object is a dictionary where each key represents a cloud service provider, and the corresponding value is another dictionary containing information about their services.

To convert the `data` object to JSON format, we use the `json.dumps()` function, which converts a Python object to a JSON-formatted string.

Finally, we print the JSON data using the `print()` function. This should produce output that looks similar to the following:

```bash
{
    "aws": {
        "service": "ec2",
        "description": "Elastic Compute Cloud"
    },
    "azure": {
        "service": "VM",
        "description": "Virtual Machines"
    },
    "gcp": {
        "service": "compute engine",
        "description": "Compute Engine"
    }
}
```

Note that the exact output may vary depending on the contents of the `services.yaml` file.