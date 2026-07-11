---
date : '2026-06-12'
draft : false
slug : 'numpy'
categories : 'Python Data Science'
summary: 'Fundamentals of NumPy (Numerical Python), an open-source Python library designed for efficient numerical computing and data processing.'
description: 'NumPy (Numerical Python) is an open-source Python library designed for efficient numerical computing and data processing.'
author : 'Ika Utami'
tags :
    - "Data Science Libraries"
series:
    - "Data Science"
title : 'Numpy Fundamentals'
ShowReadingTime: true
ShowPostNavLinks: true
---


## 1. What is NumPy?

NumPy (Numerical Python) is an open-source Python library designed for efficient numerical computing and data processing. It provides a powerful data structure called the **ndarray (N-dimensional array)**, which allows users to store and manipulate large collections of numerical data more efficiently than Python's built-in lists.

One of NumPy's greatest strengths is its ability to perform mathematical operations on entire arrays simultaneously through **vectorized operations**. Instead of using explicit `for` loops, users can apply arithmetic operations directly to an array, resulting in cleaner code and significantly faster execution, especially when working with large datasets.

In addition to multidimensional arrays, NumPy offers a rich collection of functions for performing mathematical calculations, statistical analysis, linear algebra, matrix operations, Fourier transforms, and random number generation. These capabilities make NumPy an essential tool for scientific computing and data analysis.

NumPy serves as the foundation of the Python data science ecosystem. Many popular libraries, including **Pandas**, **Matplotlib**, **Seaborn**, **Scikit-learn**, **TensorFlow**, and **PyTorch**, are built on top of NumPy or use its array structure for efficient computation. As a result, learning NumPy is often the first step toward mastering data science, machine learning, and artificial intelligence with Python.

### A. Installing NumPy

Install NumPy using pip.

```bash
pip install numpy
```
### B. Importing NumPy

By convention, NumPy is imported using the alias **np**.

```python
import numpy as np
```

## 2. Creating Arrays

### A. One-Dimensional Array

```python
import numpy as np

numbers = np.array([10, 20, 30, 40, 50])

print(numbers)
```

**Output**

```text
[10 20 30 40 50]
```



### B. Two-Dimensional Array

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(matrix)
```

**Output**

```text
[[1 2 3]
 [4 5 6]]
```



## 3. Array Attributes

```python
matrix = np.array([
    [1,2,3],
    [4,5,6]
])

print(matrix.ndim)
print(matrix.shape)
print(matrix.size)
print(matrix.dtype)
```

**Output**

```text
2
(2, 3)
6
int64
```

> **Note:** The data type (`dtype`) may vary depending on your operating system (e.g., `int32` on Windows).



## 4. Creating Arrays Automatically

### A. Zeros

```python
zeros = np.zeros((2,3))

print(zeros)
```

**Output**

```text
[[0. 0. 0.]
 [0. 0. 0.]]
```



### B. Ones

```python
ones = np.ones((3,2))

print(ones)
```

**Output**

```text
[[1. 1.]
 [1. 1.]
 [1. 1.]]
```



### C. Range of Numbers

```python
numbers = np.arange(1,11)

print(numbers)
```

**Output**

```text
[ 1  2  3  4  5  6  7  8  9 10]
```



### D. Evenly Spaced Numbers

```python
numbers = np.linspace(0, 1, 5)

print(numbers)
```

**Output**

```text
[0.   0.25 0.5  0.75 1.  ]
```



## 5. Accessing Array Elements

```python
numbers = np.array([10,20,30,40,50])

print(numbers[0])
print(numbers[3])
print(numbers[-1])
```

**Output**

```text
10
40
50
```



## 6. Slicing Arrays

```python
numbers = np.array([10,20,30,40,50,60])

print(numbers[1:4])
print(numbers[:3])
print(numbers[3:])
```

**Output**

```text
[20 30 40]
[10 20 30]
[40 50 60]
```



## 7. Modifying Array Elements

```python
numbers = np.array([10,20,30])

numbers[1] = 99

print(numbers)
```

**Output**

```text
[10 99 30]
```



## 8. Mathematical Operations

```python
numbers = np.array([1,2,3,4])

print(numbers + 5)
print(numbers * 2)
print(numbers / 2)
print(numbers ** 2)
```

**Output**

```text
[6 7 8 9]
[2 4 6 8]
[0.5 1.  1.5 2. ]
[ 1  4  9 16]
```



## 9. Arithmetic Between Arrays

```python
a = np.array([1,2,3])

b = np.array([4,5,6])

print(a + b)
print(a * b)
```

**Output**

```text
[5 7 9]
[ 4 10 18]
```



## 10. Statistical Functions

```python
scores = np.array([80,90,85,95,70])

print(np.mean(scores))
print(np.max(scores))
print(np.min(scores))
print(np.sum(scores))
print(np.std(scores))
```

**Output**

```text
84.0
95
70
420
8.602325267
```



## 11. Reshaping Arrays

```python
numbers = np.arange(1,13)

matrix = numbers.reshape(3,4)

print(matrix)
```

**Output**

```text
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```



## 12. Random Numbers

```python
random_numbers = np.random.randint(1,11,size=5)

print(random_numbers)
```

**Possible Output**

```text
[4 8 2 9 6]
```

> Since the numbers are generated randomly, your output may be different.



## 13. Practical Example

Calculate students' average score.

```python
import numpy as np

scores = np.array([78, 85, 90, 88, 92])

average = np.mean(scores)

highest = np.max(scores)

lowest = np.min(scores)

print("Scores :", scores)
print("Average:", average)
print("Highest:", highest)
print("Lowest :", lowest)
```

**Output**

```text
Scores : [78 85 90 88 92]
Average: 86.6
Highest: 92
Lowest : 78
```



## 14. Common Errors

### A. Forgetting to Import NumPy

```python
numbers = np.array([1,2,3])
```

**Error**

```text
NameError: name 'np' is not defined
```

**Solution**

```python
import numpy as np
```



### B. Shape Mismatch

```python
a = np.array([1,2,3])

b = np.array([1,2])

print(a + b)
```

**Error**

```text
ValueError: operands could not be broadcast together
```

The arrays must have compatible shapes.

