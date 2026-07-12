---
date : '2026-06-12'
draft : false
slug : 'file-handling'
categories : 'Python Programming'
summary: 'A beginner-friendly guide to Python file handling.'
description: 'Learn how to read and write files and work with file paths in Python.'
author : 'Ika Utami'
tags :
    - "Python Programming"
series:
    - "Python Basics"
title : 'File Handling in Python'
ShowReadingTime: true
ShowPostNavLinks: true
---

## File Handling in Python

File handling allows Python programs to **store data permanently** by reading from and writing to files. Unlike variables, whose values are lost when a program ends, files retain data on disk for future use.

Python provides built-in functions for file operations and supports working with various file types such as text files, CSV files, JSON files, images, and binary files.

Typical file operations include:

- Reading existing files
- Writing new files
- Appending data to files
- Managing file paths
- Checking file existence



## Opening Files

Before reading or writing a file, it must be opened using the `open()` function.

```python
file = open("example.txt", "r")
```

Syntax:

```python
open(filename, mode)
```

Common file modes:

| Mode | Description |
|------|-------------|
| `"r"` | Read (default) |
| `"w"` | Write (overwrite existing file) |
| `"a"` | Append to existing file |
| `"x"` | Create a new file |
| `"rb"` | Read binary file |
| `"wb"` | Write binary file |
| `"r+"` | Read and write |



## Reading Files

Reading files is one of the most common tasks in Python. It allows programs to retrieve previously stored information.

### Reading the Entire File

```python
file = open("example.txt", "r")

content = file.read()

file.close()

print(content)
```

Suppose **example.txt** contains:

```text
Python
Programming
Language
```

Output

```text
Python
Programming
Language
```



### Using the `with` Statement

The recommended approach is to use the `with` statement because it automatically closes the file.

```python
with open("example.txt", "r") as file:
    content = file.read()

print(content)
```



### Reading One Line

```python
with open("example.txt", "r") as file:
    line = file.readline()

print(line)
```

Output

```text
Python
```



### Reading All Lines

```python
with open("example.txt", "r") as file:
    lines = file.readlines()

print(lines)
```

Output

```text
['Python\n', 'Programming\n', 'Language']
```



### Reading Line by Line

```python
with open("example.txt") as file:
    for line in file:
        print(line.strip())
```

Output

```text
Python
Programming
Language
```



## Writing Files

Writing files allows a program to save information for later use.

### Writing a New File

The `"w"` mode creates a new file or overwrites an existing one.

```python
with open("output.txt", "w") as file:
    file.write("Hello Python!")
```

Contents of **output.txt**

```text
Hello Python!
```



### Writing Multiple Lines

```python
lines = [
    "Python\n",
    "Java\n",
    "C++\n"
]

with open("languages.txt", "w") as file:
    file.writelines(lines)
```

Contents

```text
Python
Java
C++
```



### Appending to a File

The `"a"` mode adds content without deleting existing data.

```python
with open("output.txt", "a") as file:
    file.write("\nWelcome to File Handling.")
```

Contents

```text
Hello Python!
Welcome to File Handling.
```



### Creating a File

The `"x"` mode creates a new file and raises an error if it already exists.

```python
with open("newfile.txt", "x") as file:
    file.write("New file created.")
```



## Working with File Paths

Python provides the `pathlib` module, which offers a modern and platform-independent way to work with file paths.

Import the module:

```python
from pathlib import Path
```



### Creating a Path

```python
from pathlib import Path

file_path = Path("data/example.txt")

print(file_path)
```

Output

```text
data/example.txt
```



### Checking Whether a File Exists

```python
from pathlib import Path

file_path = Path("example.txt")

print(file_path.exists())
```

Output

```text
True
```

or

```text
False
```



### Checking Whether It Is a File

```python
from pathlib import Path

path = Path("example.txt")

print(path.is_file())
```



### Checking Whether It Is a Directory

```python
from pathlib import Path

path = Path("documents")

print(path.is_dir())
```



### Getting File Name

```python
from pathlib import Path

path = Path("documents/report.pdf")

print(path.name)
```

Output

```text
report.pdf
```



### Getting File Extension

```python
from pathlib import Path

path = Path("documents/report.pdf")

print(path.suffix)
```

Output

```text
.pdf
```



### Getting File Name Without Extension

```python
from pathlib import Path

path = Path("documents/report.pdf")

print(path.stem)
```

Output

```text
report
```

---

### Getting the Parent Directory

```python
from pathlib import Path

path = Path("documents/report.pdf")

print(path.parent)
```

Output

```text
documents
```



### Creating Directories

```python
from pathlib import Path

folder = Path("data")

folder.mkdir(exist_ok=True)
```

The directory is created if it does not already exist.



### Listing Files in a Directory

```python
from pathlib import Path

folder = Path(".")

for file in folder.iterdir():
    print(file)
```



### Joining Paths

```python
from pathlib import Path

folder = Path("data")

file_path = folder / "students.txt"

print(file_path)
```

Output

```text
data/students.txt
```



## Practical Examples

### Example 1: Copy a Text File

```python
with open("input.txt", "r") as source:
    content = source.read()

with open("copy.txt", "w") as destination:
    destination.write(content)
```



### Example 2: Count the Number of Lines

```python
with open("example.txt") as file:
    count = len(file.readlines())

print("Total lines:", count)
```

Output

```text
Total lines: 3
```



### Example 3: Save User Input

```python
name = input("Enter your name: ")

with open("users.txt", "a") as file:
    file.write(name + "\n")
```



### Example 4: Read Only Existing Files

```python
from pathlib import Path

path = Path("example.txt")

if path.exists():
    with open(path) as file:
        print(file.read())
else:
    print("File not found.")
```



## Common Errors

### Error 1: File Not Found

```python
with open("missing.txt") as file:
    print(file.read())
```

Output

```text
FileNotFoundError
```

Solution:

```python
from pathlib import Path

path = Path("missing.txt")

if path.exists():
    with open(path) as file:
        print(file.read())
```



### Error 2: Forgetting to Close a File

Incorrect:

```python
file = open("example.txt")

content = file.read()
```

Better:

```python
with open("example.txt") as file:
    content = file.read()
```

The `with` statement automatically closes the file.



### Error 3: Overwriting Existing Data

```python
with open("notes.txt", "w") as file:
    file.write("New content")
```

The `"w"` mode removes all previous contents.

If you want to preserve existing data, use `"a"` instead.



### Best Practices

- Always use the `with` statement when working with files.
- Use `pathlib.Path` instead of manually constructing file paths.
- Check whether files exist before reading them.
- Use `"a"` mode when adding data instead of replacing it.
- Close files properly to avoid resource leaks.
- Handle exceptions for more robust programs.



## Summary

Python provides simple yet powerful tools for working with files. You can **read** data using `read()`, `readline()`, and `readlines()`, **write** data using `write()` and `writelines()`, and safely manage files using the `with` statement. The `pathlib` module simplifies working with file paths, directories, and file metadata in a platform-independent way. Mastering file handling is an essential skill for building real-world Python applications that process and persist data.