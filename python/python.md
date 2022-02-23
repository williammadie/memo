# Python

## Table of Contents
- [Python Package Index PIP](#python-package-index-pip)
    - [What is PIP ?](#what-is-pip)
    - [PIP commands](#pip-commands)
- [Basic Objects](#basic-objects)
    - [List](#list)
- [Basic File Manipulations](#basic-file-manipulations)
- [Amazing Tools](#amazing-tools)
    - [Zip](#zip)
    - [Unzip](#unzip)
    - [Any](#any)
    - [All](#all)
    - [Map Objects](#map-objects)
- [Python Nested Functions](#python-nested-functions)
- [Scraping & Parsing](#scraping--parsing)
    - [Libraries](#libraries)
    - [Scraping](#scraping)
    - [Parsing](#parsing)
- [Python for Data Science](#python-for-data-science)
    - [Pandas](#pandas)
        - [DataFrames](#dataframes)

## Python Package Index (PIP)

### What is PIP ?

PIP is a package manager written in Python. It is used to install **python packages**. It relies on a massive online hub of public packages called the **Python Package Index**. PIP comes preinstalled with Python 2.7.9 and later versions.

![img_2](/python/resources/pip.png)

### PIP commands

Installs a package
```bash
pip3 install package-name
```

Upgrades a package
```bash
pip3 install package-name --upgrade
```

Uninstalls a package
```bash
pip3 install package-name
```

Removes all packages (if used in a venv, affects only the venv)
```bash
pip freeze | xargs pip uninstall -y
```

Installs a specific version of a package
```bash
pip3 install package-name==x.x.x
```

Lists all versions available
```bash
pip3 install package-name==
```

## Basic Objects

### List

In each and every example, we'll take the below list as a starting point:

```python
l = ['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog']
```

Returns the index of the specific element (first one matching)
```python
>>> l.index('dog')
1
```

Adds the element to the end of the list
```python
>>> l.append('duck')
['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog', 'duck']
```

Adds all the elements of the second list at the end of the first one
```python
>>> l.extend(['zebra', 'dolphin', 'sheep'])
['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog', 'zebra', 'dolphin', 'sheep']
```

Adds the element at the specified index
```python
>>> l.insert(2, 'bird') #inserts at the third position
['cat', 'dog', 'bird', 'rabbit', 'horse', 'dog', 'dog']
```

Removes the first matching element
```python
>>> l.remove('rabbit')
['cat', 'dog', 'horse', 'dog', 'dog']
```

Counts the number of occurences of the matching elements
```python
>>> l.count('dog')
3
```

Removes and returns the element at the given index
```python
>>> l.pop(3)
'horse'
```

Reverses all the elements of the list
```python
>>> l.reverse()
['dog', 'dog', 'horse', 'rabbit', 'dog', 'cat']
```

**WARNING**: please consider the fact the l.sort(), l.reverse(), l.clear() do not return any value. Instead, it modifies directly the original list.

Sorts a list by ascending order
```python
>>> l.sort()
['cat', 'dog', 'dog', 'dog', 'horse', 'rabbit']
```

Sorts a list by descending order
```python
>>> l.sort(reverse=True)
['rabbit', 'horse', 'dog', 'dog', 'dog', 'cat']
```

Copies a list
```python
>>> l2 = l.copy()   #M1: using the copy() method
>>> l2 = l[:]       #M2: using slicing
>>> l2.append('fox')
['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog'] #l
['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog', 'fox'] #l2
```

Points to another list (modify one will modify the other)
```python
>>> l3 = l
>>> l.append('fox')
['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog', 'fox'] #l
['cat', 'dog', 'rabbit', 'horse', 'dog', 'dog', 'fox'] #l3
```

Clears all items from a list
```python
>>> l.clear()
[]
```
## Basic file manipulations

Get the content of a directory and its subdirectories
```python
import os

for root, dirs, files in os.walk(target_dir):
    for dir in dirs:    #get all subdirectories
        ...
    for file in files:  #get all files
        ...
```

Get the path of a file located in the project directory
```python
>>> os.path.join(os.path.dirname(__file__), 'my_data_file.json')
'.../my_project/my_data_file.json
```

```
my_project
├── file1.py
├── file2.py
└── my_data_file.json
```
## Amazing Tools

### Zip

The **Zip** function is a built-in function that returns a iterator made from n iterables. The returned iterator is composed of tuples. Each ith tuple is composed of elements from the ith rank of each iterable.

Example:
```python
>>> fruits = ['Bananas', 'Lemons', 'Strawberries']
>>> numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(zip(fruits, numbers))
[('Bananas', 1), ('Lemons', 2), ('Strawberries', 3)]
```

We can also spot that the zip function stops at the end of the shortest iterable. If we want to stop at the end of the longest
iterable, we can use the **zip_longest()** function from the *itertools* module.

One of the most common use cases for the Zip function is to traverse lists in parallel.

Example:
```python
>>> fruits = ['Bananas', 'Lemons', 'Strawberries']
>>> numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
for f, n in zip(fruits, numbers):
    print(f"{f} and {n}")
Bananas and 1
Lemons and 2
Strawberries and 3
```

### Unzip

The **Zip** function is also used for unzipping iterables of tuples. We simply need to add the *unpacking operator: \**.
```python
>>> it = [("French", 1), ("German", 2), ("Russian", 3)]
>>> nationalities, numbers = zip(*it)
>>> nationalities
("French", "German", "Russian")
>>> numbers
(1, 2, 3)
```

### Any

The **Any** function checks if **any elements** in an iterable is **true**. It is incredibely useful when you have to check if only a single element meets a requirement. 

If only *one element* meets the requirement, the function will return True.

```python
>>> any([False, False, False])
False
>>> any([False, True, False])
True
```

### All

The **All** function checks if **all elements** in an iterable are **true**. It is incredibely useful when you have to check if a n elements meet a requirement. 

If only *one element* doesn't meet the requirement, the function will return False.

```python
>>> all([True, True, True])
True
>>> all([True, True, False])
False
```

For instance, the following block of code is building a list of dates from a dictionary. Then, it checks if each date is in a dataframe.

```python
dates = list(map(lambda x: x.split(' ')[0], exams.keys()))
res = all([(id_random, d) in df.index for d in dates if pd.Timestamp(d) <= max_date])
```
### Map objects

Beware of these objects. They have their very own behavior and can sometimes be
difficult to understand. **Map objects** are created after a `map()` function
was called as in the example below:

```python
map(lambda x: os.path.exists(x), my_iterable)
```

A call to the `map()` function returns a **Map object** which cannot be used as an iterable directly. For instance, it is not possible to write: `len(map(...))`. It will results in an error.

So why is it like that ?

The **Map object** has to been seen like a *temporary state*. It cannot be used as is with iterables' function. First it needs to be cast as a *list, set...* like that:

```python
list(map(lambda x: os.path.exists(x), my_iterable))
```

Another important thing to know is that **Map objects** modifications will modify directly the object. It will not return another object and keep the original object unchanged. It is because of its *temporary state*, it is not meant to be used several times
```python
object1 = map(lambda x: os.path.exists(x), my_iterable)
object2 = filter(lambda x: x is not None, object1)      #After this operation, the content of object1 will no longer exists
```
## Python Nested Functions

A ***nested function*** is a function defined inside a function (see example below). By default, nested functions can access variables from the enclosing function (here *print_msg()*) in **read-only mode**.

```python
def print_msg(msg):
    def printer():
        print(msg)
    printer()

>>> print_msg('Hi !')
'Hi !'
```


## Scraping & Parsing

### Libraries

```bash
pip3 install html5lib
pip3 install lxml
pip3 install requests
pip3 install bs4
```

### Scraping

Send a HTTP request to a website and get the code response:
```python
from requests import get
url = 'https://www.imdb.com/search/title?release_date=2017&sort=num_votes,desc&page=1'
response = get(url)
```

### Parsing

Get the tables from a website:
```python
import pandas as pd
import numpy as np

pd.read_html(file_path) #file_path can be replaced by a URL
```

## Python for Data Science

### Pandas

#### DataFrames

A DataFrame is a **common data structure** in Data Science. It is shaped like a 2-dimensional array (rows and columns). It is much like a spreadsheet.

Initialize a DataFrame
```python
data = [
    ['value_r1c1', 'value_r1c2', 'value_r1c3'],
    ['value_r2c1', 'value_r2c2', 'value_r2c3'],
    ['value_r3c1', 'value_r3c2', 'value_r3c3'],
]
pd.DataFrame(
    data, 
    columns=['header_col1', 'header_col2', 'header_col3']
)
```

When we focus on a specific column (or on specific columns), we obtain a **slice of the DataFrame**. It is no more a proper DataFrame. It is considered as a **Series**. It has its own properties. For instance, here, I get a slice of the DataFrame

```python
>>> df['header_col2']
>>> type(df['header_col2'])
<class 'pandas.core.series.Series'>
```
## Knowledge

- It is possible to create temporary files or folders with the **tempfile** module
- It is possible to write proper date with the **humanize** module