---
date : '2026-06-13'
draft : false
slug : 'matplotlib'
categories : 'Python Data Science'
summary: 'A beginner-friendly guide to creating charts with Matplotlib.'
description: 'Learn the basics of data visualization in Python using Matplotlib.'
author : 'Ika Utami'
tags :
    - "Data Science Libraries"
series:
    - "Data Science"
title : 'Matplotlib Introduction'
ShowReadingTime: true
ShowPostNavLinks: true
---

## Introduction to Matplotlib and Seaborn

Data visualization is an essential part of data analysis because it helps us understand patterns, trends, and relationships in data. Python provides several libraries for creating visualizations, with **Matplotlib** and **Seaborn** being the most popular.

- **Matplotlib** is a comprehensive plotting library that provides complete control over figures and axes.
- **Seaborn** is built on top of Matplotlib and offers attractive statistical graphics with less code.


## 1. Matplotlib

### A. What is Matplotlib?

Matplotlib is the "grandfather" library of data visualization with Python. It was created by John Hunter. He created it to try to replicate MatLab's (another programming language) plotting capabilities in Python. So if you happen to be familiar with matlab, matplotlib will feel natural to you. It is an excellent **2D and 3D graphics library for generating scientific figures**.

Some of the major Pros of Matplotlib are:
- Generally easy to get started for simple plots
- Support for custom labels and texts
- Great control of every element in a figure
- High-quality output in many formats
- Very customizable in general

Matplotlib allows you to create reproducible figures programmatically. Let's learn how to use it! Before continuing this lecture, I encourage you just to explore the official Matplotlib web page: http://matplotlib.org/

### B. Advantages

- Highly customizable
- Supports many chart types
- Works well with NumPy and Pandas
- Foundation for many visualization libraries

### C. Importing Matplotlib
Import the matplotlib.pyplot module under the name plt (the tidy way):

```python
import matplotlib.pyplot as plt
```

You'll also need to use this line to see plots in the notebook:

```python
%matplotlib inline
```
That line is only for jupyter notebooks, if you are using another editor, you'll use: plt.show() at the end of all your plotting commands to have the figure pop up in another window.

### D. Basic Example
Let's walk through a very simple example using two numpy arrays:
Example: Let's walk through a very simple example using two numpy arrays. You can also use lists, but most likely you'll be passing numpy arrays or pandas columns (which essentially also behave like arrays).

**The data we want to plot:**
```python
import numpy as np
x = np.linspace(0, 5, 11)
y = x ** 2
```
**Show x:**
```
x
```
**Output:**
```
array([0. , 0.5, 1. , 1.5, 2. , 2.5, 3. , 3.5, 4. , 4.5, 5. ])
```
**Show y:**
```
y
```
**Output:**

```
array([ 0.  ,  0.25,  1.  ,  2.25,  4.  ,  6.25,  9.  , 12.25, 16.  ,
       20.25, 25.  ])
```

### E. Basic Matplotlib Commands
We can create a very simple line plot using the following ( I encourage you to pause and use Shift+Tab along the way to check out the document strings for the functions we are using).

#### Code:

```python
plt.plot(x, y, 'r') # 'r' is the color red
plt.xlabel('X Axis Title Here')
plt.ylabel('Y Axis Title Here')
plt.title('String Title Here')
plt.show()
```

#### Output:

{{< figure
  src="output1.png"
  alt="Basic Example"
  align="center"
  caption="Basic Matplotlib Output"
>}}

### F. Creating Multiplots on Same Canvas

#### Code:

```python
# plt.subplot(nrows, ncols, plot_number)
plt.subplot(1,2,1)
plt.plot(x, y, 'r--') # More on color options later
plt.subplot(1,2,2)
plt.plot(y, x, 'g*-');
```

#### Output:

{{< figure
  src="output2.png"
  alt="Basic Example"
  align="center"
  caption="Creating Multiplots on Same Canvas"
>}}

### G. Matplotlib Object Oriented Method
Now that we've seen the basics, let's break it all down with a more formal introduction of Matplotlib's Object Oriented API. This means we will instantiate figure objects and then call methods or attributes from that object. 

The main idea in using the more formal Object Oriented method is to create figure objects and then just call methods or attributes off of that object. This approach is nicer when dealing with a canvas that has multiple plots on it.

To begin we create a figure instance. Then we can add axes to that figure:

#### Code:

```python
# Create Figure (empty canvas)
fig = plt.figure()

# Add set of axes to figure
axes = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # left, bottom, width, height (range 0 to 1)

# Plot on that set of axes
axes.plot(x, y, 'b')
axes.set_xlabel('Set X Label') # Notice the use of set_ to begin methods
axes.set_ylabel('Set y Label')
axes.set_title('Set Title')
```

#### Output:

{{< figure
  src="output3.png"
  alt="Basic Example"
  align="center"
  caption="Object Oriented Method"
>}}

Code is a little more complicated, but the advantage is that we now have full control of where the plot axes are placed, and we can easily add more than one axis to the figure:

#### Code:

```python
# Creates blank canvas
fig = plt.figure()

axes1 = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # main axes
axes2 = fig.add_axes([0.2, 0.5, 0.4, 0.3]) # inset axes

# Larger Figure Axes 1
axes1.plot(x, y, 'b')
axes1.set_xlabel('X_label_axes2')
axes1.set_ylabel('Y_label_axes2')
axes1.set_title('Axes 2 Title')

# Insert Figure Axes 2
axes2.plot(y, x, 'r')
axes2.set_xlabel('X_label_axes2')
axes2.set_ylabel('Y_label_axes2')
axes2.set_title('Axes 2 Title');
```

#### Output:

{{< figure
  src="output4.png"
  alt="Basic Example"
  align="center"
  caption="More Complicated Visualization with Matplotlib"
>}}

### H. Subplot()
The plt.subplots() object will act as a more automatic axis manager. Basic use cases:

#### Code:

```python
# Use similar to plt.figure() except use tuple unpacking to grab fig and axes
fig, axes = plt.subplots()

# Now use the axes object to add stuff to plot
axes.plot(x, y, 'r')
axes.set_xlabel('x')
axes.set_ylabel('y')
axes.set_title('title');
```

#### Output:

{{< figure
  src="output5.png"
  alt="Basic Example"
  align="center"
  caption="Subplot with Matplotlib"
>}}

Then you can specify the number of rows and columns when creating the subplots() object:

#### Code:

```python
# Empty canvas of 1 by 2 subplots
fig, axes = plt.subplots(nrows=1, ncols=2)
```

#### Output:

{{< figure
  src="output6.png"
  alt="Basic Example"
  align="center"
  caption="Subplot with Matplotlib"
>}}

We can iterate through this array:

#### Code:
```python
for ax in axes:
    ax.plot(x, y, 'b')
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_title('title')

# Display the figure object    
fig
```

#### Output:

{{< figure
  src="output7.png"
  alt="Basic Example"
  align="center"
  caption="Subplot with Matplotlib"
>}}

A common issue with matplolib is overlapping subplots or figures. We ca use fig.tight_layout() or plt.tight_layout() method, which automatically adjusts the positions of the axes on the figure canvas so that there is no overlapping content:

#### Code:
```python
fig, axes = plt.subplots(nrows=1, ncols=2)

for ax in axes:
    ax.plot(x, y, 'g')
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_title('title')

fig    
plt.tight_layout()
```

#### Output:

{{< figure
  src="output8.png"
  alt="Basic Example"
  align="center"
  caption="Subplot with Matplotlib"
>}}

### I. Figure size, aspect ratio and DPI
Matplotlib allows **the aspect ratio, DPI and figure size** to be specified when the Figure object is created. You can use the figsize and dpi keyword arguments.
- figsize is a tuple of the width and height of the figure in inches.
- dpi is the dots-per-inch (pixel per inch).

For example:
```python
fig = plt.figure(figsize=(8,4), dpi=100)
```

```python
fig, axes = plt.subplots(figsize=(12,3))

axes.plot(x, y, 'r')
axes.set_xlabel('x')
axes.set_ylabel('y')
axes.set_title('title');
```

#### Output:
{{< figure
  src="output9.png"
  alt="Basic Example"
  align="center"
  caption="Figure size, aspect ratio and DPI in Matplotlib"
>}}


### J. Saving Figure
Matplotlib can generate high-quality output in a number formats, including PNG, JPG, EPS, SVG, PGF and PDF.

To save a figure to a file we can use the savefig method in the Figure class:
```python
fig.savefig("filename.png")
```
Here we can also optionally specify the DPI and choose between different output formats:
```python
fig.savefig("filename.png", dpi=200)
```

### K. Legends, labels and titles
Now that we have covered the basics of how to create a figure canvas and add axes instances to the canvas, let's look at how decorate a figure with titles, axis labels, and legends.

```python
ax.set_title("title");
ax.set_xlabel("x")
ax.set_ylabel("y");
```

You can use the label="label text" keyword argument when plots or other objects are added to the figure, and then using the legend method without arguments to add the legend to the figure:

```python
fig = plt.figure()

ax = fig.add_axes([0,0,1,1])

ax.plot(x, x**2, label="x**2")
ax.plot(x, x**3, label="x**3")
ax.legend()
```
#### Output:
{{< figure
  src="output10.png"
  alt="Basic Example"
  align="center"
  caption="Adding Legends in Matplotlib"
>}}

### L. Setting colors, linewidths, linetypes
Matplotlib gives you a lot of options for customizing colors, linewidths, and linetypes.

There is the basic MATLAB like syntax (which I would suggest you avoid using for more clairty sake:

With matplotlib, we can define the colors of lines and other graphical elements in a number of ways. First of all, we can use the MATLAB-like syntax where 'b' means blue, 'g' means green, etc. The MATLAB API for selecting line styles are also supported: where, for example, 'b.-' means a blue line with dots:

```python
# MATLAB style line color and style 
fig, ax = plt.subplots()
ax.plot(x, x**2, 'b.-') # blue line with dots
ax.plot(x, x**3, 'g--') # green dashed line
```
#### Output:
{{< figure
  src="output11.png"
  alt="Basic Example"
  align="center"
  caption="Setting colors, linewidths, linetypes in Matplotlib"
>}}

## 2. Special Plot Types
There are many specialized plots we can create, such as barplots, histograms, scatter plots, and much more. Most of these type of plots we will actually create using seaborn, a statistical plotting library for Python. But here are a few examples of these type of plots:

### A. Scatter Plot
```python
plt.scatter(x,y)
```
#### Output:
{{< figure
  src="output12.png"
  alt="Basic Example"
  align="center"
  caption="Scatterplot in Matplotlib"
>}}



### B. Histogram
```python
from random import sample
data = sample(range(1, 1000), 100)
plt.hist(data)
```
#### Output:
{{< figure
  src="output13.png"
  alt="Basic Example"
  align="center"
  caption="Histogram in Matplotlib"
>}}

### C. Boxplot
```python
data = [np.random.normal(0, std, 100) for std in range(1, 4)]

# rectangular box plot
plt.boxplot(data,vert=True,patch_artist=True);   
```

#### Output:
{{< figure
  src="output14.png"
  alt="Basic Example"
  align="center"
  caption="Boxplot in Matplotlib"
>}}

## Further reading
- http://www.matplotlib.org - The project web page for matplotlib.
- https://github.com/matplotlib/matplotlib - The source code for matplotlib.
- http://matplotlib.org/gallery.html - A large gallery showcaseing various types of plots matplotlib can create. Highly recommended!
- http://www.loria.fr/~rougier/teaching/matplotlib - A good matplotlib tutorial.
- http://scipy-lectures.github.io/matplotlib/matplotlib.html - Another good matplotlib reference.



