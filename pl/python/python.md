# Python

## Table of Contents
- [Python](#python)
- [CPython PyPy and Cython](#cpython-pypy-and-cython)
- [Python and Performance](#python-and-performance)
- [Python Package Index PIP](#python-package-index-pip)
- [Packaging](#packaging)
- [Python for Scripting](#python-for-scripting)
    - [Call the script](#call-the-script)
    - [Get rid of python](#get-rid-of-python)
    - [Keep running](#keep-running)
    - [Use OS commands](#use-os-commands)
- [Basic Objects and Functions](#basic-objects-and-functions)
    - [Builtin Tools](#builtin-tools)
        - [Numbers](#numbers)
        - [Strings](#strings)
    - [Print](#print)
    - [List](#list)
    - [List Comprehension](#list-comprehension)
    - [Set](#set)
- [Basic File Manipulations](#basic-file-manipulations)
- [Basic Date and Time Handling](#basic-date-and-time-handling)
    - [Read & Write](#read-write)
    - [Manipulate files](#manipulate-files)
    - [Manipulate ZIP files](#manipulate-zip-files)
- [Amazing Tools](#amazing-tools)
- [Python OOP](#python-oop)
- [Python Nested Functions](#python-nested-functions)
- [Scraping & Parsing](#scraping--parsing)
- [Python for Data Science](#python-for-data-science)
- [Debugging](#debugging)
- [Python Settings and Environment](#python-settings-and-environment)
- [Knowledge](#knowledge)
- [Coding Problem Solutions](#coding-problem-solutions)
- [Write better code](#write-better-code)
    - [Python Enhancement Proposal (PEP)](#python-enhancement-proposal-pep)
    - [Naming Conventions](#naming-conventions)
    - [Comments & Docstrings](#comments-and-docstrings)
    - [Spaces, Indentations & Line breaks](#spaces-indentations--line-breaks)
    - [Good Practices](#good-practices)
    - [Formatter & Linter](#formatter-&-linter)
        - [Install a Linter on VSCode](#install-a-linter-on-vscode)
        - [Disable the Linter on VSCode](#disable-the-linter-on-vscode)

## Python

Python is a **Programming Language** (PL). It has several implementations. The default one which is also the most widely used is called `CPython` but there are also `PyPy`, `Jython` and more!

Most of these different implementations use the same **Runtime Engine** which is called `Python Virtual Machine` (PVM). The PVM's role is to read Byte Code and make use of the Operating System's calls to complete tasks.

Let's see in details two of these implementations.

## CPython PyPy and Cython

### CPython

`CPython` is the **default implementation** of the Python Programming Language. It uses an **AoT compiler** for compiling `Python Source Code` to `Python Byte Code` which is a more efficient language for the PVM.

Python is sometimes refered as an `interpreted language`. It is actually false as the most widely implementation uses an **AoT compiler**. But where does this idea comes from ? People say that because `CPython` uses **automatic compilation** which is done at runtime. So this compilation step is hidden from the final user.

But wait, I should be able to see this compilation step: compilation always takes a long time, no?

Yes and no, the `CPython` compiler does very little checks at compile time so it is actually very fast.

![cpython-implementation](/pl/python/resources/cpython-implementation.png)

### PyPy

`PyPy` is an alternative implementation of the Python PL. It uses an **AoT compiler** and a **JiT compiler** to improve the performance of some parts of the program.

It also uses **automatic compilation**, so the process is hidden from the final user. The first step is the compilation from `Python Source Code` to `Python Byte Code` and the second one is the compilation from `Byte Code` to `Machine Code` (=binary).

![pypy-implementation](/pl/python/resources/pypy-implementation.png)

### Cython

`Cython` **is not a Python Implementation**. It is tool used to optimize specific parts of a Python program. It is used to compile `Python Source Code` to `C` or `C++` code and to make it a shared library then usable inside Python programs.

## Python and Performance

Since the dawn of time, it has always been pointed out that Python was slow. However, nowadays Python is one of the most learned and used languages in the world.

It took me several years to understand how a inefficient language like Python could be so influent in Computer Science. First I thought that the answer was really simple and could be summarized in one sentence :

**Productivity over Raw Performance**

- Productivity would be the time to write code that executes a specific task.
- Raw Performance would be the time taken by the code to execute.

This sentence is false in general. However, in specific domains such as *Data Science* it is true. In my career, I have come accross several cases where we would use Python to write our program and then simply upgrade our hardware so that it would run properly.

However, it is not always the case as for an algorithm written in C and Python time complexity will be the same and hardware would barely make no difference.

This leads me to understand another important aspect of Python:

**Ease of use and Community**

Python is one of the few languages that programmers and non-programmers can use at a daily bases. The learning curve is extremely fast compared to other languages and the languages offers an interface towards more optimized code. Here is where the community comes on stage.

In Data Science, we have some incredibly powerful libraries such as **numpy**, **pandas**, **tensorflow** and more recently **polars**. These libaries are not written in Python. They are written in Cython (Compiled Python code) or even in C, C++ and Rust which are today's most efficient languages. And here is one of the most useful strengths of Python:

**An Interface towards other languages**

When people say that Python is slow, they think about the language itself which is slow due to its **dynamic** nature (=types are determined at runtime). However, Python is blazing fast when dealing with large datasets, doing computations and machine learning because of this interface ability.

So would you still say that Python is slow?

Another important thing I've learned the hard way:

*Shitty code will always be slow independtly from the language you've chosen. Write efficient code before thinking to switching to another language*

## Python Package Index (PIP)

### What is PIP ?

PIP is a package manager written in Python. It is used to install **python packages**. It relies on a massive online hub of public packages called the **Python Package Index**. PIP comes preinstalled with Python 2.7.9 and later versions.

![img_2](/pl/python/resources/pip.png)

### PIP commands

Upgrade PIP
```bash
pip install --upgrade pip
```

Show version of a specific package
```bash
pip3 list | grep package-name
```

Installs a package
```bash
pip3 install package-name
```

Installs a package in development mode
(You have to be inside the repo of the project before
running the command)
```bash
pip3 install -e .
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

## Packaging

Build a Python Package
```python
python -m pip install --upgrade pip build
python3 -m build
```

Install a Package from TestPyPi
```python
pip install -i https://test.pypi.org/pypi/ my-package-name

# OR if the package has dependencies 

python3 -m pip install --index-url https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple/ your-package
```

If pip does not find any package, update it to its last version with the following command
```py
python3 -m pip install --upgrade pip setuptools wheel
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

### Use OS commands

It is very useful to communicate with your Operating System and specifically to use your OS commands in a Python script. How can you do that? It is very simple, let me show you:

Below is a function that use the command `echo df /path/to/folder | sftp -b - hostname | awk {print $3/1024/1024} | tail -n 1` to get the available size of a folder on a remote server. It uses 4 commands with pipes.
```py
def sftp_get_available_size() -> float:
  """Get available size of the SFTP"""
  echo = ['echo', 'df', 'path/to/folder']
  sftp = ['sftp', '-b', '-', 'hostname']
  awk = ['awk', '{print $3/1024/1024}']
  tail = ['tail', '-n', '1']

  p1 = subprocess.Popen(echo, stdout=subprocess.PIPE)
  p2 = subprocess.Popen(sftp, stdin=p1.stdout, stdout=subprocess.PIPE)
  p1.stdout.close()
  p3 = subprocess.Popen(awk, stdin=p2.stdout, stdout=subprocess.PIPE)
  p2.stdout.close()
  p4 = subprocess.Popen(tail, stdin=p3.stdout, stdout=subprocess.PIPE)
  p3.stdout.close()

  output = p4.communicate()[0].decode('utf8')
  output = output.replace('\n', '') if '\n' in output else output
  return float(output) 
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

### List Comprehension

A Python list comprehension provides a very short syntax **for creating a new list based on the values of an existing list**. It is visually distinguishable because it is a one-liner syntax consisting of **square brackets containing the expression**:

An exemple of list comprehension which creates a new list containing lengths of all city names
```python
# [output collection condition]
>>> city_names = ["New York", "Paris", "London"]
>>> length_of_names = [len(city_name) for city_name in city_names]
[8, 5, 6]
```

List comprehension with an if statement
```python
[transform(value) for value in df["column1"] if condition]
```

List comprehension with an if-else statement
```python
[transform(value) if condition else value for value in df["column1"]]
```

### Set

A **set** is a bit like a list. It is a collection of objects **without any duplicates**. It is not possible to add an object which is already present in a given set. It is very useful when we want to use the **Set Theory** and all its operations.

Instanciate a set
```python
s = set()   # For instanciation with known values, use the second form
# OR
s = {4}
s = {'source'}
```

Add an object to a set
```python
s.add(31)
```

Remove an object from a set
```python
s.remove(31)
```

Get the intersection of two sets
```python
s1.intersection(s2)
```

Get the union of two sets
```python
s1.union(s2)
```

Get the difference between two sets
```python
s1.difference(s2)
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

Check if a file exists
```python
>>> os.path.exists(filename)
True
```

Find the shortest common prefix of a string list
```python
>>> os.path.commonprexif(['DD101-0512', 'DD101-1203', 'DD101-1300'])
'DD101'
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

### Manipulate ZIP files

Add a file to a ZIP Archive
```py
with zipfile.ZipFile(zip_archive_name, 'w', compression =  zipfile.ZIP_DEFLATED) as zipf:
      with zipf.write(file2add, arcname='filename-in-archive') as file:
```

List files in a ZIP Archive
```py
with zipfile.ZipFile(zip_archive_name) as zipf:
    files = file.namelist()
```

Read a file in a ZIP Archive
```py
with zipfile.ZipFile(zip_archive_name) as zipf:
      with zipf.open(internal_file_to_read) as file:
        lines = file.readlines()
```

## Basic Date and Time Handling

In order to properly handle dates and time, you need to use the `datetime` package. It lets you work on dates very easily by identifying and modifying years, months, days, hours, minutes, seconds and even timezones.

Import the builtin package dedicated to handling date and time
```python
from datetime import datetime
```

Convert a string to a datetime object
```python
date = datetime.strptime(str_date, '%Y-%m-%d %H:%M:%S')
```

Convert a datetime object to a string
```python
str_date = datetime.strftime(date, '%Y-%m-%d %H:%M:%S')
```

Replace an attribute of the datetime object
```py
'2016-03-16 09:45:32'
>>> date = date.replace(hour=0, minute=0, second=0)
'2016-03-16 00:00:00'
```


## Amazing Tools

### Star Operator

The `*` operator can be used for functions which takes an infinite number of parameters:

```python
def sum_all(*args):
    result = 0
    for num in args:
        result += num
    return result
```

It can also be used with integers in arithmetical operations but it is not its only use ! It can also be used with strings and collections :

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

### Star Star Operator

Yeah, it isn't its real name. 

`**` can be used to obtain all **named arguments** of a function (those passed like `my_arg = value`).

Following the same principle, it can also be used to merge dictionaries:
```python
res_dic = {**dic1, **dic2, **dic3}
```

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
### Dataclasses

**Dataclasses** are a special kind of classes used primarily for **storing information**. They hold certain properties (= attributes) and methods to build a data representation.

```python
@dataclass
class ConstantsNamespace():
	self.JSON_EXT = ".json"
	self.CSV_EXT = ".csv"
	self.PYTHON_EXT = ".py"
	self.JAVA_EXT = ".java"
	self.COMPILED_JAVA_EXT = ".class"
	
# It can be used anywhere else with:
constants = ConstantsNamespace()
print(constants.COMPILED_JAVA_EXT)
>>> ".class"
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

##### Introducing DataFrames

A DataFrame is a **common data structure** in Data Science. It is shaped like a 2-dimensional array (rows and columns). It is much like a spreadsheet.

When we focus on a specific column (or on specific columns), we obtain a **slice of the DataFrame**. It is no more a proper DataFrame. It is considered as a **Series**. It has its own properties. For instance, here, I get a slice of the DataFrame

```python
>>> df['header_col2']
>>> type(df['header_col2'])
<class 'pandas.core.series.Series'>
```

##### Working with DataFrames

Creata an empty DataFrame
```python
df = pd.DataFrame()
```

Create a DataFrame and fill it with data
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

Create a DataFrame form a dictionary
```python
data = {'col1': list_of_values, 'col2': list_of_values...}
pd.DataFrame(data)

# or

df = pd.DataFrame.from_dict(data)
```

See only specific columns
```python
df[['isco08', 'number_of_hospital_staff']]
```

Replace a value at a given row and column
```python
df.at[row, column_name] = new_value
```

Aggregate by columns and sum column n4
```python
df.groupby(['column1', 'c2', 'cn'])[['n4']].sum().reset_index()
```

Get a DataFrame from a CSV file
```python
import pandas as pd
df = pd.read_csv('path/to/df.csv')
```

Save a DataFrame as a CSV file
```python
df.to_csv('path/to/df.csv')
```

See all columns name
```python
df.columns.values
```

See number of entries, number of columns, columns names, memory usage
```python
df.info()
```

See first entries of the DataFrame
```python
df.head()
```

See last entries of the DataFrame
```py
df.tail()
```

See most common values in a column
```py
df.values_count()
```

Search for rows where a given column contains a given value
```python
df[df['column1'] == value]
```

Keep only given columns
```python
df = df[['country', 'date']]
```

Fill a column with a given value
```python
df.loc[:, 'age_group'] = np.nan
df.loc[:, 'city'] = 'New York'
```

(Note)
Should I use `np.nan` or `pd.NA`?

=> If you really have to use NaN (Not a Number), **use the one from numpy**.
It is said explicitely in the documentation of **pandas** that `pd.NA` is
an experimental feature and that operations done with this value can behave
unexpectedly (boolean operations) 

Delete given columns
```python
df.drop(columns=['country', 'date'])
```

Rename given columns
```python
df = df.rename(
    columns={
        'location': 'country',
        'date': 'iso_week',
        'excess_proj_all_ages': 'excess_death'
    }
)
```

Apply a function on a given column (here we convert the date into the iso_week)
```python
df['date'] = df['date'].apply(get_iso_week)
```

Replace a value if given condition is checked (Here we only keep the row containing the country, date and age_group of a given line in a referential)
```python
df.loc[
    (df['country'] == ref['country'][i]) & (df['date'] == ref['date'][i]) & (df['age_group'] == age_df),
    'excess_death'
] = ref[f'p_scores_{age}'][i]

# Simplified:

df.loc[condition, column2modify] = new_value
df.loc[(condition1) & (condition2) & (condition3), column2modify] = new_value
```

Get the Union of n DataFrames
(Please note: it is advised to use build a new DataFrame and the use pd.concat than use the df.append() method due to an important difference in time complexity of such operation if used in a loop)
```python
import pandas as pd
concatenated_df = pd.concat([df1, df2, df3, dfn])
```

Keep rows where value for column X is in a list
```python
df = df[df['country'].str.lower().isin(EU_COUNTRIES)]
```

Keep rows where value for column X is NOT in a list
(Tilde is the NOT operator in dataframe queries)
```python
df = df[~df['country'].str.lower().isin(EU_COUNTRIES)]
```

Build a new column based on values in other columns
```python
# This function is called for determining the value at each row of the new column
def build_column(row: pd.Series, facility: str, base_column: str) -> pd.DataFrame:
    return row[base_column] if row["facility"] == facility else None

df["number_of_icu_beds"] = df.apply(lambda x: build_column(x, "HBEDT_CUR", "number_of_hospital_beds"), axis=1)
```

Split the column X in two or more different columns based on values inside columns X
```python
# 1.If we want to have two final columns then, create two dataframes.
# Filter them from the original one so you have your values separated
df_all = df[df["TargetGroup"] == "ALL"].reset_index()
df_population = df[df["TargetGroup"].str.lower().isin(["hcw","ltcf"])].reset_index()

# 2. Rename the columns
df_all.rename(columns={"TargetGroup": "AgeGroup"}, inplace=True)
df_population.rename(columns={"TargetGroup": "TargetPopulation"}, inplace=True)

# (optional: do the modifications you want)
# Here we'd like two have NaN on all rows with HCW or LTCF
df_all.loc[:, "TargetPopulation"] = np.nan
df_all.loc[:, "AgeGroup"] = np.nan


# 3. Merge the two dataframes to retrieve the original dataframe format
pd.concat([df_all, df_population])
```

### Keep in Mind when Dealing with DataFrame

![time-complexity](/pl/python/resources/time-complexity-operations-df.png)

### Hashlib

Get the hash of a value:
```python
digest = int(hashlib.sha512(my_string.encode('utf-8')).hexdigest(), 16)
```

**WARNING : DO NOT USE THE hash() FUNCTION. It is depreciated: since Python 3.3, the hash() function use randomization and so the Determinism property is broken (only one and unique result for a input value)**

## Debugging

One of the simplest way of debugging in Python is to use the `print()` function where we need to visualize information in order to understand the problem. However, there are more convenient ways of debugging in Python.

The first way of debugging which is incredibely better than a print and not more difficult is the `breakpoint()` function. This function can be used anywhere we need in our code. It will stop the execution of the program and open a Python interpreter called `Pdb (Python Debugger)`. 

In this Python interpreter, we will be able to visualize all the declared variables. We can find these variables with `dir()`.
Here is a list of all useful commands in Pdb:

- `dir()`: list all currently declared/available variables
- `l`: (list) show surrounding lines
- `w`: (where) display the file name and the line number of the current line
- `n`: (next) execute the next line
- `s`: (step) step into function
- `r`: (return) execute until function's return
- `b [line_number]`: create a breakpoint at given line
- `clear [line_number]`: remove a breakpoint at given line
- `b`: list breakpoints and theirs line number
- `c`: (continue) continue execution until next breakpoint or end of program
- `p <variable>`: print the value of a given variable
- `q`: (quit) exit the debugger

It can also be useful to set a condition before calling `breakpoint()`. It is called a **conditional breakpoint**.

*Note:* `dir()` can also be used to show all methods from an object at any time (debugguer or not)

## Python Settings and Environment

### PATH

If you have a custom installation of Python, you may be interested in knowing what is the Python **PATH**. For instance, you have Python 2.5.1 installed on your computer for a bunch of projects. A new project requires you to install Python 3.8.7. You cannot simply delete Python 2 and install Python 3. There is a gap between those 2 versions and no backward compatibility. So what can be done?

It is possible to install another version of Python. You will simply need to show where it is to your computer. To do that, you can use the **PATH** environment variable. It is a string of concatenated paths separated with `:`. **These paths are folders which contain binaries (=executable files). It allows the computer to locate/use all available binaries**. 

For instance, it can look like this:

```bash
PATH=/space/hadoop/lib/python-3.6.7-lib/bin:/space/hadoop/lib/python-3.6.7-lib/bin:/home/william2/.vscode-server/bin/30d9c6cd9483b2cc586687151bcbcd635f373630/bin/remote-cli:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

If you need to locate your new version of Python, you can use the `whereis` command like `whereis python-3.x.x`

To modify the Python **PATH** variable, you will use the command:

```bash
export PATH=”$PATH:/usr/local/bin/python”
```

In this command, you update the **PATH** by adding a new path (/usr/local/bin/python). You keep all old paths by specifying the `$PATH:` before your new one. The `:` is used to delimit each path.

### Virtual Environment

A **virtual environment** is an isolated environment where pythonic developers like to work. It allows them to easily manage Python dependencies on all their projects and prevents incompatibilities.

For instance, a project can require to have `numpy==3.2.4`, `easyocr==16.0.1` and `pytorch==23.0.1` where another will require `numpy==5.6.1` and `pytorch==21.0.5`. In this case, if the developers did not use **virtual environments**, he is screwed. With virtual environments, each project has its own dependencies and each dependency has its own version. This significantly decreases the risk of conflicts between them.

Create a virtual environment
```bash
python3 -m venv env
```

Activate the virtual environment
```bash
. env/bin/activate
```

Deactivate the virtual environment
```bash
deactivate
```

Virtual environments **MUST NOT** be added to version control. It is always heavy and can contain secrets.


## Knowledge

- It is possible to create temporary files or folders with the **tempfile** module
- It is possible to write proper date with the **humanize** module
- Create APIs with **fastapi** or **Flask**

## Coding Problem Solutions

### String

Count how many vowels are in a word (AEIOU)
```python
print(*map(s.count,'AEIOU'))
```

## Write Better Code

### Python Enhancement Proposal (PEP)

The **Python Enhancement Proposal** also known as **PEP** is a bunch of documents which describes new functionalities, process and environments for Python.

The **PEP 8** is the most used PEP. It is *a guide style* and also a reference of good practices for Python developers

### Naming conventions

```python
# variables

full_name = 'John Doe'
fruits = ['banana', 'apple', 'peach']

# constants

DAYS_PER_WEEK = 7
PASTORAL_INDEX = 'Z.T.67'

# classes

class BigElephant:
    pass

class StrangeHuman:
    pass

# modules (builtin example)

import os
import sys
import shutil
import pathlib
```

### Comments and Docstrings

Comments should be written on their own line separated from the code. They should also be on the same level of indentation than the following line of code.

```python
# this is a comment

def my_function():
    blabla
    if blabla:
        # this is a good comment
        blabla
```

Docstrings refer to commented parts using `"""blabla"""`. According to PEP257, they should be used the most possible. It is a very good practice for quality and help on a project.

Docstrings are a way of taking a step back on what we're doing. It can be used at the beginning of modules, classes and functions.

Docstrings **do not describe the internal mechanisms of the function**. Instead, they indicate what is returned by the function.

```python
"""This function calculates and returns the mean of ..."""  # one-line docstring

"""This function caculates and returns the mean of ...

Attrs:
- parameter n°1...
- parameter n°2...

Returns:
- object returned...
""" # multi-line docstring
```

### Spaces, Indentations & Line breaks

In Python, we use spaces or indentations but we do not mix them together in the same project. Standard says the size of an indent should be *4 spaces*.

- Before defining a class or a function there should be a break of *2 lines*. 

- Before defining a method inside a class there should be a break of *1 line*

- Lines should not be longer than 79 characters.

For a long function declaration use:
```python
def my_very_long_function_name(
    parameter1,
    parameter2,
    parameter3
):
    blabla
    return blabla
```

### Good Practices

For functions:
- return types should always be identical (or None) for all the `return` inside the function.
- Use `return None` instead of `return`

For slicing str:
- Use `str.startswith() or str.endswith()` instead of slicing. For more advanced problems, use *regex*.

For try/except:
- A try/except block should cover the less possible lines in order to avoid hiding other issues/bugs.
- You should never use a bare except. It increases the risk of letting critical errors pass.

### Formatter & Linter

A formatter is a little program that will fix your code according to the standard of a programming langage. It is purely *focused on syntax (and can even break your code)*.

A linter is another program charged to spot *standard non-compliant part of your code*. It is a very powerful tool that can also indicate depreciated practices in your code.

#### Install a Linter on VSCode

1. `CTRL + SHIFT + P` to show the command palette
2. Type `python: select linter`
3. Select *Flake8* (Auto-download starts)
4. Enjoy

#### Disable the Linter on VSCode

1. `CTRL + SHIFT + P` to show the command palette
2. Type `python: disable linter`

(more at: https://code.visualstudio.com/docs/programming_languages/python/linting)
