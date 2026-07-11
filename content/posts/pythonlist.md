---
date : '2026-07-11'
draft : false
slug : 'python-list'
categories : 'Data Structure'
author : 'Ika Utami'
tags :
    - "Python Data Structure"
title : 'Python List Data Structure'
ShowReadingTime: true
ShowPostNavLinks: true
---
## Introduction to Lists

A list is one of the most commonly used data structures in Python. It is an ordered, mutable collection of items, meaning that the elements are stored in a specific sequence and can be modified after the list is created. Lists are versatile because they can store multiple values of different data types within a single variable.

For example, a list can contain integers, floating-point numbers, strings, Boolean values, and even other lists. This flexibility makes lists suitable for representing collections such as student names, exam scores, shopping items, or sensor readings.

## Characteristics of Lists
- **Ordered** – Elements maintain their insertion order.
- **Mutable** – Elements can be modified after creation.
- **Indexed** – Elements are accessed using zero-based indexing.
- **Dynamic** – Lists can grow or shrink during program execution.
- **Heterogeneous** – Different data types can be stored in the same list.
- **Duplicates Allowed** – Lists can contain duplicate values.

# Creating Lists

Lists are created using square brackets `[]` with items separated by commas.

```python
# Empty list
empty_list = []

# List of integers
numbers = [10, 20, 30, 40]

# List of strings
fruits = ["Apple", "Banana", "Orange"]

# Mixed data types
student = ["Alice", 21, 3.85, True]

print(numbers)
print(fruits)
print(student)
```

Output

```text
[10, 20, 30, 40]
['Apple', 'Banana', 'Orange']
['Alice', 21, 3.85, True]
```

---

# Accessing List Elements

Each element has an index beginning from **0**.

```python
fruits = ["Apple", "Banana", "Orange", "Mango"]

print(fruits[0])
print(fruits[2])
print(fruits[-1])
```

Output

```text
Apple
Orange
Mango
```

### Index Illustration

| Index | 0 | 1 | 2 | 3 |
|-------|---|---|---|---|
| Value | Apple | Banana | Orange | Mango |

Negative indexing starts from the end.

| Index | -4 | -3 | -2 | -1 |
|-------|----|----|----|----|
| Value | Apple | Banana | Orange | Mango |

---

# Modifying List Elements

Lists are mutable, meaning elements can be changed.

```python
fruits = ["Apple", "Banana", "Orange"]

fruits[1] = "Mango"

print(fruits)
```

Output

```text
['Apple', 'Mango', 'Orange']
```

Adding new elements:

```python
fruits.append("Grape")
print(fruits)
```

Output

```text
['Apple', 'Mango', 'Orange', 'Grape']
```

Removing elements:

```python
fruits.remove("Orange")
print(fruits)
```

Output

```text
['Apple', 'Mango', 'Grape']
```

---

# List Methods

Python provides many useful methods for manipulating lists.

| Method | Description |
|---------|-------------|
| `append(x)` | Add an item to the end |
| `insert(i, x)` | Insert an item at a specific position |
| `extend(iterable)` | Add multiple items |
| `remove(x)` | Remove the first matching item |
| `pop()` | Remove and return an item |
| `clear()` | Remove all elements |
| `index(x)` | Find the position of an item |
| `count(x)` | Count occurrences |
| `sort()` | Sort the list |
| `reverse()` | Reverse the list |
| `copy()` | Create a shallow copy |

Example

```python
numbers = [5, 3, 8, 1]

numbers.sort()
print(numbers)

numbers.reverse()
print(numbers)
```

Output

```text
[1, 3, 5, 8]
[8, 5, 3, 1]
```

---

# Slicing Lists

Slicing extracts part of a list.

Syntax

```python
list[start:stop:step]
```

Example

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:4])
print(numbers[:3])
print(numbers[3:])
print(numbers[::2])
```

Output

```text
[20, 30, 40]
[10, 20, 30]
[40, 50, 60]
[10, 30, 50]
```

---

# Iterating Over Lists

Lists are commonly processed using loops.

Using a `for` loop:

```python
fruits = ["Apple", "Banana", "Orange"]

for fruit in fruits:
    print(fruit)
```

Output

```text
Apple
Banana
Orange
```

Using `enumerate()`:

```python
for index, fruit in enumerate(fruits):
    print(index, fruit)
```

Output

```text
0 Apple
1 Banana
2 Orange
```

---

# List Comprehensions

List comprehensions provide a concise way to create new lists.

General syntax

```python
new_list = [expression for item in iterable if condition]
```

Example 1

```python
numbers = [1, 2, 3, 4, 5]

squares = [n**2 for n in numbers]

print(squares)
```

Output

```text
[1, 4, 9, 16, 25]
```

Example 2

```python
even = [n for n in numbers if n % 2 == 0]

print(even)
```

Output

```text
[2, 4]
```

---

# Nested Lists

A list can contain other lists.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[1][2])
```

Output

```text
6
```

Traversing a nested list:

```python
for row in matrix:
    for value in row:
        print(value, end=" ")
    print()
```

Output

```text
1 2 3
4 5 6
7 8 9
```

---

# Practical Examples and Common Errors

## Example 1: Calculate Average Score

```python
scores = [80, 90, 75, 95]

average = sum(scores) / len(scores)

print("Average:", average)
```

Output

```text
Average: 85.0
```

---

## Example 2: Find the Largest Number

```python
numbers = [12, 5, 33, 18]

largest = max(numbers)

print(largest)
```

Output

```text
33
```

---

## Example 3: Remove Duplicate Values

```python
numbers = [1, 2, 2, 3, 4, 4, 5]

unique = list(set(numbers))

print(unique)
```

---

## Common Error 1: Index Out of Range

```python
numbers = [10, 20, 30]

print(numbers[5])
```

Error

```text
IndexError: list index out of range
```

**Solution:** Check the length of the list before accessing an index.

```python
if len(numbers) > 5:
    print(numbers[5])
```

---

## Common Error 2: Using Parentheses Instead of Brackets

Incorrect

```python
numbers = (1, 2, 3)
numbers.append(4)
```

Error

```text
AttributeError: 'tuple' object has no attribute 'append'
```

**Solution**

```python
numbers = [1, 2, 3]
numbers.append(4)
```

---

## Common Error 3: Modifying a List While Iterating

Incorrect

```python
numbers = [1, 2, 3, 4]

for n in numbers:
    if n % 2 == 0:
        numbers.remove(n)

print(numbers)
```

Better approach

```python
numbers = [1, 2, 3, 4]

numbers = [n for n in numbers if n % 2 != 0]

print(numbers)
```

Output

```text
[1, 3]
```

---

# Summary

Python lists are powerful and flexible containers for storing collections of data. They support indexing, slicing, iteration, nesting, and a rich collection of built-in methods. Mastering lists is essential because they are widely used in data processing, algorithm implementation, web development, machine learning, and many other Python applications.
