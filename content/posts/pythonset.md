---
date : '2026-07-11'
draft : false
slug : 'python-set'
categories : 'Data Structure'
summary: 'A comprehensive guide to Python Sets for beginners.'
description: 'Learn Python sets, including creation, operations, methods, set algebra, and practical examples.'
author : 'Ika Utami'
tags :
    - "Python Data Structure"
series:
  - "Python Basics"
title : 'Python Sets Data Structure'
ShowReadingTime: true
ShowPostNavLinks: true
ShowToc: true
TocOpen: true
---

# Introduction to Sets

A **set** is an unordered collection of unique elements in Python. Unlike lists and tuples, sets do not allow duplicate values and do not maintain the order of insertion.

Sets are particularly useful when you need to:

- Remove duplicate values
- Perform mathematical set operations
- Check membership efficiently
- Compare collections of data

## Characteristics of Sets

- Unordered collection
- Mutable (elements can be added or removed)
- Contains only unique elements
- Cannot contain mutable objects like lists or dictionaries
- Supports fast membership testing
- Implements mathematical set operations

Example:

```python
fruits = {"apple", "banana", "orange"}

print(fruits)
```

Output

```text
{'apple', 'banana', 'orange'}
```

> **Note:** Since sets are unordered, the display order may vary each time the program runs.

---

# Creating Sets

## Empty Set

Use the `set()` function.

```python
empty_set = set()

print(type(empty_set))
```

Output

```text
<class 'set'>
```

Using `{}` creates a dictionary instead.

```python
empty = {}

print(type(empty))
```

Output

```text
<class 'dict'>
```

---

## Set with Elements

```python
numbers = {10, 20, 30, 40}

print(numbers)
```

---

## Creating a Set from a List

```python
numbers = [1, 2, 2, 3, 4, 4, 5]

unique_numbers = set(numbers)

print(unique_numbers)
```

Output

```text
{1, 2, 3, 4, 5}
```

---

## Creating from a String

```python
letters = set("programming")

print(letters)
```

Possible output

```text
{'p', 'r', 'o', 'g', 'a', 'm', 'i', 'n'}
```

---

# Accessing Set Elements

Sets do **not** support indexing or slicing.

Incorrect:

```python
numbers = {10, 20, 30}

print(numbers[0])
```

Output

```text
TypeError: 'set' object is not subscriptable
```

Instead, iterate through the set.

```python
numbers = {10, 20, 30}

for number in numbers:
    print(number)
```

---

# Adding Elements

## add()

Adds a single element.

```python
numbers = {1, 2, 3}

numbers.add(4)

print(numbers)
```

Output

```text
{1, 2, 3, 4}
```

---

## update()

Adds multiple elements.

```python
numbers = {1, 2}

numbers.update([3, 4, 5])

print(numbers)
```

Output

```text
{1, 2, 3, 4, 5}
```

---

# Removing Elements

## remove()

Removes an element.

```python
numbers = {1, 2, 3}

numbers.remove(2)

print(numbers)
```

Output

```text
{1, 3}
```

If the element does not exist:

```python
numbers.remove(10)
```

Output

```text
KeyError
```

---

## discard()

Removes an element if it exists.

```python
numbers = {1, 2, 3}

numbers.discard(10)

print(numbers)
```

No error occurs.

---

## pop()

Removes and returns an arbitrary element.

```python
numbers = {1, 2, 3}

value = numbers.pop()

print(value)
print(numbers)
```

---

## clear()

Removes all elements.

```python
numbers = {1, 2, 3}

numbers.clear()

print(numbers)
```

Output

```text
set()
```

---

# Set Operations

## Union

Combines two sets.

```python
A = {1, 2, 3}
B = {3, 4, 5}

print(A | B)
print(A.union(B))
```

Output

```text
{1, 2, 3, 4, 5}
```

---

## Intersection

Returns common elements.

```python
A = {1, 2, 3}
B = {2, 3, 4}

print(A & B)
```

Output

```text
{2, 3}
```

---

## Difference

Returns elements only in the first set.

```python
A = {1, 2, 3}
B = {2, 3, 4}

print(A - B)
```

Output

```text
{1}
```

---

## Symmetric Difference

Returns elements in either set but not both.

```python
A = {1, 2, 3}
B = {3, 4, 5}

print(A ^ B)
```

Output

```text
{1, 2, 4, 5}
```

---

# Membership Testing

```python
fruits = {"apple", "banana", "orange"}

print("banana" in fruits)
print("grape" in fruits)
```

Output

```text
True
False
```

---

# Set Methods

Some commonly used methods include:

| Method | Description |
|---------|-------------|
| `add()` | Add one element |
| `update()` | Add multiple elements |
| `remove()` | Remove an element |
| `discard()` | Remove safely |
| `pop()` | Remove arbitrary element |
| `clear()` | Remove all elements |
| `copy()` | Create a copy |
| `union()` | Combine sets |
| `intersection()` | Common elements |
| `difference()` | Elements only in first set |
| `symmetric_difference()` | Non-common elements |
| `issubset()` | Check subset |
| `issuperset()` | Check superset |
| `isdisjoint()` | Check whether sets have no common elements |

Example:

```python
A = {1, 2}
B = {1, 2, 3}

print(A.issubset(B))
print(B.issuperset(A))
```

Output

```text
True
True
```

---

# Frozen Sets

A **frozenset** is an immutable version of a set.

```python
numbers = frozenset([1, 2, 3])

print(numbers)
```

Output

```text
frozenset({1, 2, 3})
```

Since it is immutable:

```python
numbers.add(4)
```

Output

```text
AttributeError
```

---

# Practical Examples

## Example 1: Remove Duplicates

```python
scores = [80, 90, 80, 95, 90, 100]

unique_scores = list(set(scores))

print(unique_scores)
```

---

## Example 2: Find Common Courses

```python
student1 = {"Math", "Physics", "Programming"}
student2 = {"Programming", "English", "Math"}

common = student1 & student2

print(common)
```

Output

```text
{'Math', 'Programming'}
```

---

## Example 3: Unique Words

```python
sentence = "python is fun and python is powerful"

words = set(sentence.split())

print(words)
```

---

# Common Errors

## Error 1: Duplicate Values

```python
numbers = {1, 2, 2, 3, 3}

print(numbers)
```

Output

```text
{1, 2, 3}
```

Duplicates are automatically removed.

---

## Error 2: Using Mutable Objects

Incorrect:

```python
numbers = {[1, 2], [3, 4]}
```

Output

```text
TypeError: unhashable type: 'list'
```

Correct:

```python
numbers = {(1, 2), (3, 4)}

print(numbers)
```

---

## Error 3: Assuming Order

Incorrect:

```python
colors = {"red", "green", "blue"}

print(colors)
```

The output order is **not guaranteed**.

---

# When to Use Sets

Use a set when you need to:

- Remove duplicate values
- Perform union, intersection, or difference operations
- Check membership efficiently
- Compare collections of unique items

Avoid using sets when:

- Element order matters
- Duplicate values must be preserved
- Index-based access is required

---

# Summary

Python **sets** are mutable, unordered collections of unique elements. They are ideal for eliminating duplicates, performing mathematical set operations, and efficiently checking membership. Understanding sets is essential for writing cleaner, faster, and more efficient Python programs, especially when working with collections of unique data.