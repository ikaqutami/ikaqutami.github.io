---
date : '2026-07-11'
draft : false
slug : 'python-dictionary'
categories : 'Data Structure'
summary: 'A comprehensive guide to Python dictionaries for beginners.'
description: 'Learn Python dictionaries, including creating, accessing, modifying, iterating, dictionary methods, comprehensions, nested dictionaries, and practical examples.'
author : 'Ika Utami'
tags :
    - "Python Data Structure"
series:
  - "Python Basics"
title : 'Python Dictionaries'
ShowReadingTime: true
ShowPostNavLinks: true
---

## Introduction to Dictionaries

A **dictionary** is a built-in Python data structure that stores data as **key-value pairs**. Each key is unique and is used to access its corresponding value.

Unlike lists and tuples, dictionaries are optimized for fast lookups using keys instead of numeric indexes.

Dictionaries are commonly used to represent structured data such as student records, employee information, product catalogs, configuration settings, and JSON objects.

### Characteristics of Dictionaries

- Store data as **key-value pairs**
- Mutable (items can be added, modified, or removed)
- Keys must be unique
- Keys must be immutable (e.g., strings, numbers, tuples)
- Values can be any data type
- Preserve insertion order (Python 3.7+)

Example:

```python
student = {
    "name": "Alice",
    "age": 20,
    "major": "Computer Science"
}

print(student)
```

Output

```text
{'name': 'Alice', 'age': 20, 'major': 'Computer Science'}
```

---

## Creating Dictionaries

### Empty Dictionary

```python
student = {}

print(student)
```

Output

```text
{}
```

Using the constructor:

```python
student = dict()

print(student)
```

---

### Dictionary with Initial Values

```python
student = {
    "name": "John",
    "age": 21,
    "gpa": 3.8
}

print(student)
```

---

### Using the `dict()` Constructor

```python
student = dict(
    name="John",
    age=21,
    major="Computer Science"
)

print(student)
```

---

### Creating from a List of Tuples

```python
student = dict([
    ("name", "Alice"),
    ("age", 20),
    ("major", "Mathematics")
])

print(student)
```

---

## Accessing Dictionary Elements

### Using Square Brackets

```python
student = {
    "name": "Alice",
    "age": 20
}

print(student["name"])
print(student["age"])
```

Output

```text
Alice
20
```

---

### Using `get()`

```python
student = {
    "name": "Alice",
    "age": 20
}

print(student.get("name"))
print(student.get("gpa"))
```

Output

```text
Alice
None
```

Providing a default value:

```python
print(student.get("gpa", "Not Available"))
```

Output

```text
Not Available
```

---

## Modifying Dictionary Elements

### Updating a Value

```python
student = {
    "name": "Alice",
    "age": 20
}

student["age"] = 21

print(student)
```

Output

```text
{'name': 'Alice', 'age': 21}
```

---

### Adding New Key-Value Pairs

```python
student["major"] = "Computer Science"

print(student)
```

Output

```text
{
    'name': 'Alice',
    'age': 21,
    'major': 'Computer Science'
}
```

---

### Removing Elements

Using `del`

```python
del student["age"]

print(student)
```

Using `pop()`

```python
student.pop("major")
```

Using `popitem()`

```python
student.popitem()
```

Removing everything

```python
student.clear()
```

---

## Dictionary Methods

Some commonly used dictionary methods include:

| Method | Description |
|---------|-------------|
| `get()` | Retrieve a value safely |
| `keys()` | Return all keys |
| `values()` | Return all values |
| `items()` | Return key-value pairs |
| `update()` | Merge another dictionary |
| `pop()` | Remove a key |
| `popitem()` | Remove the last inserted item |
| `clear()` | Remove all items |
| `copy()` | Create a shallow copy |
| `setdefault()` | Return value or create a default |

Example:

```python
student = {
    "name": "Alice",
    "age": 20
}

print(student.keys())
print(student.values())
print(student.items())
```

Output

```text
dict_keys(['name', 'age'])
dict_values(['Alice', 20])
dict_items([('name', 'Alice'), ('age', 20)])
```

---

## Iterating Over Dictionaries

### Iterate Over Keys

```python
student = {
    "name": "Alice",
    "age": 20,
    "major": "CS"
}

for key in student:
    print(key)
```

---

### Iterate Over Values

```python
for value in student.values():
    print(value)
```

---

### Iterate Over Key-Value Pairs

```python
for key, value in student.items():
    print(key, ":", value)
```

Output

```text
name : Alice
age : 20
major : CS
```

---

## Nested Dictionaries

Dictionaries can contain other dictionaries.

```python
students = {
    "student1": {
        "name": "Alice",
        "age": 20
    },
    "student2": {
        "name": "Bob",
        "age": 22
    }
}

print(students)
```

Access nested values.

```python
print(students["student1"]["name"])
print(students["student2"]["age"])
```

Output

```text
Alice
22
```

---

## Dictionary Comprehensions

Dictionary comprehensions provide a concise way to create dictionaries.

Basic example:

```python
squares = {
    x: x**2
    for x in range(1, 6)
}

print(squares)
```

Output

```text
{
    1: 1,
    2: 4,
    3: 9,
    4: 16,
    5: 25
}
```

With conditions:

```python
even_squares = {
    x: x**2
    for x in range(10)
    if x % 2 == 0
}

print(even_squares)
```

Output

```text
{
    0: 0,
    2: 4,
    4: 16,
    6: 36,
    8: 64
}
```

---

## Practical Examples and Common Errors

### Example 1: Student Record

```python
student = {
    "name": "Alice",
    "age": 20,
    "major": "Computer Science",
    "gpa": 3.85
}

for key, value in student.items():
    print(f"{key}: {value}")
```

Output

```text
name: Alice
age: 20
major: Computer Science
gpa: 3.85
```

---

### Example 2: Word Frequency Counter

```python
sentence = "python is fun and python is powerful"

frequency = {}

for word in sentence.split():
    frequency[word] = frequency.get(word, 0) + 1

print(frequency)
```

Output

```text
{
    'python': 2,
    'is': 2,
    'fun': 1,
    'and': 1,
    'powerful': 1
}
```

---

### Example 3: Merge Dictionaries

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

dict1.update(dict2)

print(dict1)
```

Output

```text
{
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4
}
```

---

### Common Error 1: Accessing a Missing Key

Incorrect:

```python
student = {
    "name": "Alice"
}

print(student["age"])
```

Output

```text
KeyError: 'age'
```

Correct:

```python
print(student.get("age"))
```

---

### Common Error 2: Duplicate Keys

```python
student = {
    "name": "Alice",
    "name": "Bob"
}

print(student)
```

Output

```text
{'name': 'Bob'}
```

The last value replaces the previous one.

---

### Common Error 3: Using Mutable Keys

Incorrect:

```python
data = {
    [1, 2]: "numbers"
}
```

Output

```text
TypeError: unhashable type: 'list'
```

Correct:

```python
data = {
    (1, 2): "numbers"
}

print(data)
```

---

## When to Use Dictionaries

Use dictionaries when you need to:

- Store related information using descriptive keys
- Perform fast lookups by key
- Represent structured or hierarchical data
- Count frequencies or map one value to another
- Work with JSON-like data structures

Avoid using dictionaries when:

- Data should be accessed by numeric position
- Duplicate keys are required
- Maintaining repeated values under the same key is necessary (use a list instead)

---

## Summary

Python **dictionaries** are powerful, mutable collections that store data as **key-value pairs**. They provide fast access to values through unique keys and support a wide range of operations, including updating, deleting, iterating, nesting, and comprehensions. Dictionaries are one of the most commonly used data structures in Python and are essential for organizing and managing structured data efficiently.
