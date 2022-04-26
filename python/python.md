# Python

## Table of Contents
- [Python Package Index PIP](#python-package-index-pip)
    - [What is PIP ?](#what-is-pip)
    - [PIP commands](#pip-commands)
- [Python for Scripting](#python-for-scripting)
    - [Call the script](#call-the-script)
    - [Get rid of python](#get-rid-of-python)
    - [Keep running](#keep-running)
- [Basic Objects and Functions](#basic-objects-and-functions)
    - [Builtin Tools](#builtin-tools)
        - [Numbers](#numbers)
        - [Strings](#strings)
    - [Print](#print)
    - [List](#list)
- [Basic File Manipulations](#basic-file-manipulations)
    - [Read & Write](#read-write)
    - [Manipulate files](#manipulate-files)
- [Amazing Tools](#amazing-tools)
    - [Star operator](#star-operator)
    - [Zip](#zip)
    - [Unzip](#unzip)
    - [Any](#any)
    - [All](#all)
    - [Map Objects](#map-objects)
- [Python OOP](#python-oop)
- [Python Nested Functions](#python-nested-functions)
- [Scraping & Parsing](#scraping--parsing)
    - [Libraries](#libraries)
    - [Scraping](#scraping)
    - [Parsing](#parsing)
- [Python for Data Science](#python-for-data-science)
    - [Pandas](#pandas)
        - [DataFrames](#dataframes)
- [Debugging](#debugging)
- [Knowledge](#knowledge)
- [Coding Problem Solutions](#coding-problem-solutions)
    - [String](#string)

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
## Python for Scripting

### Call the script

In order to call a python script and to be able to give it arguments, we use the **argparse** and the **sys** modules.

```python
import argparse
import sys

def main(argv):
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "-i",
        "--indir",
        type=str,
        help="Path of the input directory",
        required=True)

    parser.add_argument(
        "-o",
        "--outdir",
        type=str,
        help="Path of the output directory",
        required=True)

    parser.set_defaults(func=do_job)

    # calling handlers
    func = None
    try:
        args = parser.parse_args()
        func = args.func
    except AttributeError:
        parser.print_help()
    if func is not None:
        args.func(args, parser)

def do_job(args, *other):
    job(indir=args.indir, outdir=args.outdir)

if __name__ == '__main__':
    main(sys.argv)
```

### Get rid of python

It can be pretty heavy to have to specify the **python** keyword  everytime you want to launch your script. `python3 hello.py` I agree. 
In fact, there is a way of getting rid of it.

```python
#!/usr/bin/env python3
```
```bash
chmod +x hello.py
```
By adding this line - called a ***shebang line*** - at the very beginning of our file (before the import section) and by adding the **execution rights** to your executable, you can achieve that.

Now you'll be able to call your script like the following:
```bash
/path/to/hello.py
```

The ***shebang line*** acts like a script doorkeeper. At launch, the OS will come and ask the doorkeeper how he can use the script. The doorkeeper will show him the path of the *proper excutable* (here the python executable) required to use the script. For instance, this is also used in **bash**.

No more `python` !

### Keep running

When you program in Python, you'll always want to do things like run a script **in background** or make a script run **even when you're not connected**.

Here is the command you're looking for. When the `&` is indicated, the script will run in the background. We say that it is **detached** from your terminal.
```bash
python3 coucou.py &
```

If you want that the script keeps running even if you close the terminal, you can use the linux `nohup` keyword. Of course, you can
precise where the logs must be written:
```bash
nohup python3 coucou.py > /path/to/output.log
```

Keep in mind that everything can be used together:
```bash
nohup /path/to/hello.py > /path/to/output.log &
```

## Basic Objects and Functions

### Builtin Tools

#### Numbers

Find the absolute value of a number.
```python
>>> abs(-56)
56
```

Find the **highest number** between 2 numbers of in an iterable.
```python
>>> a = [0, 1, 2, 3, 4, 5]
>>> max(a)
5
>>> max(1, 2)
2
```

Find the **lowest number** between 2 numbers of in an iterable.
```python
>>> a = [0, 1, 2, 3, 4, 5]
>>> min(a)
0
>>> min(1, 2)
1
```

Calculate the power of a number.
```python
>>> pow(2, 5)
32
```

Calculate the exponential of a number.
```python
>>> math.exp(3)
20.085536923187668
```

But wait! You have imported a library in order to do this operation, this is not a builtin function!

Yes, you're right: I have imported a library. However, the notion of builtin in Python is not limited to what exists without new imports. It depends on whether you need to install the library or not. If you haven't install the library, this is considered a builtin library.

What is the difference between **math.floor()** VS **math.ceil()** VS **int()** VS **round()**?

| initial value |                                 int()                                 |                      math.floor()                     |                 round()                 |                    math.ceil()                   |
|:-------------:|:---------------------------------------------------------------------:|:-----------------------------------------------------:|:---------------------------------------:|:------------------------------------------------:|
|       -       | rounds towards 0 (like floor for positive and like ceil for negative) | rounds towards minus infinity. Lowest possible answer | rounds to the closest possible solution | rounds towards infinity. Highest possible answer |
|      1.0      |                                   1                                   |                          1.0                          |                   1.0                   |                        1.0                       |
|      1.1      |                                   1                                   |                          1.0                          |                   1.0                   |                        2.0                       |
|      1.5      |                                   1                                   |                          1.0                          |                   2.0                   |                        2.0                       |
|      1.9      |                                   1                                   |                          1.0                          |                   2.0                   |                        2.0                       |
|      -1.1     |                                   -1                                  |                          -2.0                         |                   -1.0                  |                       -1.0                       |
|      -1.5     |                                   -1                                  |                          -2.0                         |                   -2.0                  |                       -1.0                       |
|      -1.9     |                                   -1                                  |                          -2.0                         |                   -2.0                  |                       -1.0                       |


#### Strings

Convert a string to uppercase.
```python
>>> 'What a nice car!'.upper()
'WHAT A NICE CAR!'
```

Convert a string to lowercase.
```python
>>> 'WHAT A NICE CAR!'.lower()
'What a nice car!'
```

Check if a string contains only letters (as well as special letters such as ç). Special characters and punctuation are not letters, so it will return False.
```python
>>> 'hey'.isalpha()
True
>>> 'hey1'.isalpha()
False
>>> 'hey, how you doin ?'.isalpha()
False
```

Check if a string contains **positive integers** {0, 1, 2... n}
```python
>>> '0'.isdecimal()
True
>>> '0.123'.isdecimal()
False
>>> '-16'.isdecimal()
False
>>> '16'.isdecimal()
True
```

Check if a string contains a whitespace character or a special identifier such as (`\t`, `\r`, `\n`)
```python
>>> "    ".isspace() # four spaces
True
>>> "   ".isspace() # a tab
True
>>> "\n".isspace() # newline
True
>>> "\t".isspace() # tab
True
>>> "\r".isspace() # carriage return
True
>>> "\f".isspace() # form feed
True
```

### Print

In Python, we use the **print** function to prompt information to the user.

```python
>>> print()     # returns '\n'


>>> print('Hello world!')
'Hello world!'

>>> print('Hello', 'world', '!') # prints 'Hello world !\n'
'Hello world !'
```

By default, the **print** function behaves like if it was called with the `sep`
arguments:

```python
>>> print('Hello', 'world', '!')
>>> print('Hello', 'world', '!', sep=' ')
'Hello world !'
```

By default, the **print** function automatically adds a ***newline character***
at the end of the last str:

```python
>>> print('Hello', 'world', '!') # returns 'Hello world !\n'
'Hello world !'
```

To remove the ***newline character*** with can use the `end` argument:

```python
>>> print('Hello', 'world', '!', end='') # returns 'Hello world !' with no '\n'
'Hello world !'
```

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

Sorts a list by applying a specific rule
```python
>>> l.sort(key = lambda v: v[0])
```

Here, this **key** argument can be used to sort a list made of tuples. A tuple contains n values. So we can tell Python to only consider one of these values for the sorting. In the following example, we will be sorting the tuples **by considering only their second value**:

```python
>>> l = [(3, 5, 8), (6, 2, 8), (2, 9, 4), (6, 8, 5)]
>>> l.sort(key=lambda v: v[1])
[(6, 2, 8), (3, 5, 8), (6, 8, 5), (2, 9, 4)]
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

### Read & Write

Read a file (Long version)
```python
fp = open('/path/to/mysuperfile.txt', 'r')
lines = fp.readlines()
fp.close()
```

Read a file (Short version)
```python
with open('/path/to/mysuperfile.txt', 'r') as fp:
    lines = fp.readlines()
```

In the code block above, the **with** statement is used to automatically close the file when it finishes to use it. It is closed at the end of the block.

What are the different **handling modes** for opening files?

| Mode |                                                                                                                          Description                                                                                                                          |
|:----:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|   r  |                                                                                                              Open the file in **read-only** mode.                                                                                                             |
|  r+  |                                                                                     Open the file in **read-and-write** mode. The pointer is at the beginning of the file.                                                                                    |
|  rb+ |                                                                  Open the file in **read-and-write** mode. The pointer is at the beginning of the file. This reads in the **binary format**.                                                                  |
|   w  |                           Open the file in **write** mode. The pointer is at **the beginning of the file**. If the file doesn't exist, it will be created. If the file exists, its content will be overwritten with the new content.                          |
|  w+  |                      Open the file in **read-and-write** mode. The pointer is at **the beginning of the file**. If the file doesn't exist, it will be created. If the file exists, its content will be overwritten with the new content.                      |
|  wb+ |   Open the file in **read-and-write** mode. The pointer is at **the beginning of the file**. If the file doesn't exist, it will be created. If the file exists, its content will be overwritten with the new content. This reads in the  **binary format**.   |
|   a  |                         Open the file in **write** mode. The pointer is at **the end of the file**. If the file doesn't exist, it will be created. If the file exists, the new content will be added at the end. (Does not overwrite).                        |
|  a+  |                    Open the file in **read-and-write** mode. The pointer is at **the end of the file**. If the file doesn't exist, it will be created. If the file exists, the new content will be added at the end. (Does not overwrite).                    |
|  ab+ | Open the file in **read-and-write** mode. The pointer is at **the end of the file**. If the file doesn't exist, it will be created. If the file exists, the new content will be added at the end. (Does not overwrite). This reads in the  **binary format**. |
|   x  |                      (Introduced in Python3). Open the file in **exclusive-creation-write** mode. If the file doesn't exist, it will be created. If the file exists, it will do nothing. (Useful to avoid accidentally modifying files).                      |
|  x+  |                  (Introduced in Python3). Open the file in **exclusive-creation-read-and-write** mode. If the file doesn't exist, it will be created. If the file exists, it will do nothing. (Useful to avoid accidentally modifying files).                 |
|  xb+ |   (Introduced in Python3). Open the file in **exclusive-read-and-write** mode. If the file doesn't exist, it will be created. If the file exists, it will do nothing. (Useful to avoid accidentally modifying files). This reads in the  **binary format** .  |

### Manipulate files

Build a path relying in the operating system's separators directly
```python
>>> os.path.join('dev', 'bin', 'mylog.log')
'/dev/bin/mylog.log'    # Linux
```

Get the name of the file at the end of a given filepath
```python
>>> f = '/dev/bin/mylog.log'
>>> os.path.basename(f)
'mylog.log'
```

Get the parent directory's path of a file
```python
>>> f = '/dev/bin/mylog.log'
>>> os.path.dirname(f)
'/dev/bin'
```

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

### Star Operator

In Python, the `*` operator can be used with integers in arithmetical operations but it is not its only use ! It can also be used with strings and collections ! How ? Let me tell you:

Unpacking a list:
```python
>>> print(*[0, 1, 2, 3, 4, 5, 6, 7])
0 1 2 3 4 5 6 7
```

Unpacking a string
```python
>>> print(*'Hello!')
H e l l o ! 
```

The `*` operator returns each element of the collection

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

## Python OOP

**OOP** stands for **Object Oriented Programming**. It is a popular programming paradigm used in C++, Java and many other languages. Python has its very own way to implement **OOP**. Let's dive in!

### Class and Parent Class

Creates a simple class
```python
class Dog(object):      #Python 2 & 3

    is_hairy = True

    def __init__(self, name, age, race=''):
        self.name = name
        self.age = age
        self.race = race

class Dog:      #Python 3 only

    is_hairy = True

    def __init__(self, name, age, race=''):
        self.name = name
        self.age = age
        self.race = race

d1 = Dog('Paterson', 9)
print(f'Oh look! this is {d1.name}! He is {d1.age}!')
```

Creates a class that inherits from another class
```python
class AustralianSheperd(Dog):

    def __init__(self, name, age):
        super().__init__(name, age, race='Australian Sheperd')

d1 = AustralianSheperd('Paterson', 9)
print(f'Oh look at this {d1.race}! This is {d1.name}! He is {d1.age}!')
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

## Debugging

One of the simplest way of debugging in Python is to use the `print()` function where we need to visualize information in order to understand the problem. However, there are more convenient ways of debugging in Python.

The first way of debugging which is incredibely better than a print and not more difficult is the `breakpoint()` function. This function can be used anywhere we need in our code. It will stop the execution of the program and open a Python interpreter. In this Python interpreter, we will be able to visualize all the declared variables.
We can find these variables with `dir()`

It can also be useful to set a condition before calling `breakpoint()`. It is called a **conditional breakpoint**.

## Knowledge

- It is possible to create temporary files or folders with the **tempfile** module
- It is possible to write proper date with the **humanize** module

## Coding Problem Solutions

### String

Count how many vowels are in a word (AEIOU)
```python
print(*map(s.count,'AEIOU'))
```
