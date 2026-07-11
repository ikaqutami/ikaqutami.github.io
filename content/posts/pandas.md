---
date : '2026-06-12'
draft : false
slug : 'pandas'
categories : 'Python Data Science'
summary: 'Learn the fundamentals of Pandas, including Series, DataFrames, data selection, filtering, sorting, and basic data analysis.'
description: 'Learn the fundamentals of Pandas, including Series, DataFrames, data selection, filtering, sorting, and basic data analysis.'
author : 'Ika Utami'
tags :
    - "Data Science Libraries"
series:
    - "Data Science"
title : 'Pandas Fundamentals'
ShowReadingTime: true
ShowPostNavLinks: true
---

## 1. What is Pandas?

Pandas is an open-source Python library designed for data manipulation and analysis. It provides two powerful data structures: 
- **Series**, which stores one-dimensional labeled data.
- **DataFrame**, which stores two-dimensional tabular data similar to a spreadsheet or SQL table.

Pandas simplifies tasks such as **cleaning datasets, handling missing values, filtering records, computing statistics, and preparing data for visualization and machine learning**. Built on top of NumPy, it combines high performance with an intuitive interface, making it one of the most widely used libraries in data science and analytics.



### A. Installing Pandas

Install Pandas using pip.

```bash
pip install pandas
```



### B. Importing Pandas

By convention, Pandas is imported using the alias **pd**.

```python
import pandas as pd
```



## 2. Creating a Series

A Series is a one-dimensional labeled array.

```python
import pandas as pd

ages = pd.Series([20, 22, 21, 23])

print(ages)
```

**Output**

```text
0    20
1    22
2    21
3    23
dtype: int64
```



## 3. Creating a DataFrame

A DataFrame is a two-dimensional table consisting of rows and columns.

```python
import pandas as pd

students = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [20, 21, 22],
    "Score": [85, 90, 88]
}

df = pd.DataFrame(students)

print(df)
```

**Output**

```text
      Name  Age  Score
0    Alice   20     85
1      Bob   21     90
2  Charlie   22     88
```



### A. Viewing Data

The following methods help inspect a DataFrame.

```python
print(df.head())
```

**Output**

```text
      Name  Age  Score
0    Alice   20     85
1      Bob   21     90
2  Charlie   22     88
```



```python
print(df.info())
```

**Output**

```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 3 entries, 0 to 2
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype
---  ------  --------------  -----
 0   Name    3 non-null      object
 1   Age     3 non-null      int64
 2   Score   3 non-null      int64
```



```python
print(df.describe())
```

**Output**

```text
             Age      Score
count   3.000000   3.000000
mean   21.000000  87.666667
std     1.000000   2.516611
min    20.000000  85.000000
25%    20.500000  86.500000
50%    21.000000  88.000000
75%    21.500000  89.000000
max    22.000000  90.000000
```



### B. Selecting Columns

Select a single column.

```python
print(df["Name"])
```

**Output**

```text
0      Alice
1        Bob
2    Charlie
Name: Name, dtype: object
```

Select multiple columns.

```python
print(df[["Name", "Score"]])
```

**Output**

```text
      Name  Score
0    Alice     85
1      Bob     90
2  Charlie     88
```



### C. Selecting Rows

Using **iloc** (integer position).

```python
print(df.iloc[1])
```

**Output**

```text
Name      Bob
Age        21
Score      90
Name: 1, dtype: object
```

Using **loc** (label/index).

```python
print(df.loc[0])
```

**Output**

```text
Name     Alice
Age         20
Score       85
Name: 0, dtype: object
```



### D. Filtering Data

Select students with scores greater than 85.

```python
high_scores = df[df["Score"] > 85]

print(high_scores)
```

**Output**

```text
      Name  Age  Score
1      Bob   21     90
2  Charlie   22     88
```



### E. Adding a New Column

```python
df["Passed"] = df["Score"] >= 80

print(df)
```

**Output**

```text
      Name  Age  Score  Passed
0    Alice   20     85    True
1      Bob   21     90    True
2  Charlie   22     88    True
```



### F. Modifying Data

```python
df.loc[0, "Score"] = 95

print(df)
```

**Output**

```text
      Name  Age  Score
0    Alice   20     95
1      Bob   21     90
2  Charlie   22     88
```



### G. Sorting Data

Sort by score in ascending order.

```python
print(df.sort_values("Score"))
```

**Output**

```text
      Name  Age  Score
2  Charlie   22     88
1      Bob   21     90
0    Alice   20     95
```

Sort in descending order.

```python
print(df.sort_values("Score", ascending=False))
```

**Output**

```text
      Name  Age  Score
0    Alice   20     95
1      Bob   21     90
2  Charlie   22     88
```



### H. Basic Statistics

```python
print(df["Score"].mean())
print(df["Score"].max())
print(df["Score"].min())
print(df["Score"].sum())
```

**Output**

```text
91.0
95
88
273
```



### I. Handling Missing Values

```python
students = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Score": [85, None, 90]
}

df = pd.DataFrame(students)

print(df)
```

**Output**

```text
      Name  Score
0    Alice   85.0
1      Bob    NaN
2  Charlie   90.0
```

Check missing values.

```python
print(df.isnull())
```

**Output**

```text
    Name  Score
0  False  False
1  False   True
2  False  False
```

Fill missing values.

```python
df["Score"] = df["Score"].fillna(0)

print(df)
```

**Output**

```text
      Name  Score
0    Alice   85.0
1      Bob    0.0
2  Charlie   90.0
```



### J. Grouping Data

```python
students = {
    "Department": ["IT", "IT", "CS", "CS"],
    "Score": [80, 90, 75, 85]
}

df = pd.DataFrame(students)

print(df.groupby("Department")["Score"].mean())
```

**Output**

```text
Department
CS    80.0
IT    85.0
Name: Score, dtype: float64
```



### K. Saving Data

Save a DataFrame as a CSV file.

```python
df.to_csv("students.csv", index=False)
```



## 4. Practical Example

Calculate the average score of students who passed.

```python
import pandas as pd

students = {
    "Name": ["Alice", "Bob", "Charlie", "David"],
    "Score": [85, 92, 76, 88]
}

df = pd.DataFrame(students)

passed = df[df["Score"] >= 80]

print(passed)

print("\nAverage Score:", passed["Score"].mean())
```

**Output**

```text
    Name  Score
0  Alice     85
1    Bob     92
3  David     88

Average Score: 88.33333333333333
```



## 5. Common Errors

### A. Forgetting to Import Pandas

```python
df = pd.DataFrame()
```

**Error**

```text
NameError: name 'pd' is not defined
```

**Solution**

```python
import pandas as pd
```



### B. Accessing a Non-Existent Column

```python
print(df["Grade"])
```

**Error**

```text
KeyError: 'Grade'
```

Ensure the column name exists before accessing it.



### C. Incorrect Column Name

```python
print(df["score"])
```

**Error**

```text
KeyError: 'score'
```

Remember that column names are **case-sensitive**.

