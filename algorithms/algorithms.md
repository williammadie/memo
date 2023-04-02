# Algorithms

## Table of Contents

- [Algorithm Complexity](#algorithm-complexity)
    - [Introduction](#introduction)
    - [Big O Notation](#big-o-notation)
    - [Different types of Complexity](#different-types-of-complexity)
    - [Cheat Sheet](#cheat-sheet)
- [Sorting Algorithms](#sorting-algorithms)
    - [Insertion Sort](#insertion-sort)
- [Data Structure](#data-structure)
    - [Linked List](#linked-list)
    - [FIFO](#fifo)
    - [LIFO](#lifo)
- [Recursion](#recursion)
- [Memoization](#memoization)
- [Bad Practices](#bad-practices)
- [Glossary](#glossary)

## Algorithm Complexity

### Introduction

Algorithmic complexity is a measure of **how long an algorithm would take to complete given an input of size n**. If an algorithm has to scale, it should compute the result within **a finite and practical time bound even for large values of n**. For this reason, complexity is calculated **asymptotically as n approaches infinity**.

Runtimes of algorithms can vary a lot. For instance, considering a **20 000 characters string** containing only 1 `e`, a linear search of the letter `e` will be significantly much faster if the `e` is the first letter of the string than the same operation if the `e` is at the end of the string.

This is why, **Time Complexity** is generally given is different categories: Best, Average and Worst Time Complexity.

### Big O Notation

There are 4 notations used to describe complexity:
- **Big-Oh Notation** (bounded above): most commonly used notation
- **Big-Omega Notation** (bounded below): most commonly used notation
- **Big-Theta Notation** (exactly): most commonly used notation
- **Small-o Notation** (not as expensive as): most commonly used notation

In practice, the **Big Oh** notation (or **Big O**) is the most commonly used because it is often the easier to calculate. It describes the **growth behavior of a function**. For example, a Average Time Complexity of `O(n)` means that the algorithm will have to do, in average, **n operations** to find the output.

### Different types of Complexity

**From best to worst:**
1. Constant `O(1)`: Runtime does not depend on input size
2. Logarithmic `O(log n)`: Runtime grows slower than input size
3. Linear `O(n)`: Runtime grows at the same rate as input
4. Log-Linear `O(n*log n)`: An operation of log n complexity is applied for each input value (most efficient sorting algorithm)
5. Quadratic `O(n^2)`: An operation of complexity `O(n)` is carried out for each input
6. Polynomial `O(n^3), O(n^4)...`
7. Exponential `O(2^n)`: Complexity is multiplied wich each additional input value
8. Worse `O(n!)`: Runtimes are **infinite**

Below you'll find a sum up of what is listed above:

![img1](/algorithms/resources/complexity-explained.png)

### Cheat Sheet

Here is a quick cheat sheet of the most popular algorithms and their complexity:

|      Algorithm     | Best Time Complexity | Average Time Complexity | Worst Time Complexity | Worst Space Complexity |
|:------------------:|:--------------------:|:-----------------------:|:---------------------:|:----------------------:|
|  **Linear Search** |         O(1)         |           O(n)          |          O(n)         |          O(1)          |
|  **Binary Search** |         O(1)         |         O(log n)        |        O(log n)       |          O(1)          |
|   **Bubble Sort**  |         O(n)         |          O(n^2)         |         O(n^2)        |          O(1)          |
| **Selection Sort** |        O(n^2)        |          O(n^2)         |         O(n^2)        |          O(1)          |
| **Insertion Sort** |         O(n)         |          O(n^2)         |         O(n^2)        |          O(1)          |
|   **Merge Sort**   |      O(n*log n)      |        O(n*log n)       |       O(n*log n)      |          O(n)          |
|   **Quick Sort**   |      O(n*log n)      |        O(n*log n)       |         O(n^2)        |        O(log n)        |
|    **Heap Sort**   |      O(n*log n)      |        O(n*log n)       |       O(n*log n)      |          O(n)          |
|   **Bucket Sort**  |       O(n + k)       |         O(n + k)        |         O(n^2)        |          O(n)          |
|   **Radix Sort**   |         O(nk)        |          O(nk)          |         O(nk)         |        O(n + k)        |
|    **Tim Sort**    |         O(n)         |        O(n*log n)       |       O(n*log n)      |          O(n)          |
|   **Shell Sort**   |         O(n)         |      O((n*log n)^2)     |     O((n*log n)^2)    |          O(1)          |



On the following graph, you can see the **number of operations** evolution of each complexity depending on the **number of elements in the data structure**:

![img2](/algorithms/resources/complexity-graph.png)

## Sorting Algorithms

### Insertion Sort

#### Ascending

```c
for (int i = 0; i < ARRAY_LENGTH; i++) {
        int j = i + 1;
        while (j < ARRAY_LENGTH) {
            if (*(sommes + i) > *(sommes + j)) {
                int tmp = *(sommes + i);
                *(sommes + i) = *(sommes + j);
                *(sommes + j) = tmp;
                j = i;
            }
            j++;
        }
    }
```

#### Descending

```c
for (int i = 0; i < ARRAY_LENGTH; i++) {
        int j = i + 1;
        while (j < ARRAY_LENGTH) {
            if (*(sommes + i) < *(sommes + j)) {
                int tmp = *(sommes + i);
                *(sommes + i) = *(sommes + j);
                *(sommes + j) = tmp;
                j = i;
            }
            j++;
        }
    }
```

## Data Structure

### Linked List

A Linked List memorizes the **memory address** of each element/block/node. In general, it uses 3 pointers:
- one at the head of the list (first element)
- one at the current element in the list
- one at the last element in the list

Moreover, each node points towards the next (and the previous in the case of a `Double Linked List`) elements. 

If there is no next element, it points towards `NULL`.

In a Linked List, add and remove operations are done in `O(1)`. Accessing an element is done in `O(n)` as it might requires to traverse the list from beginning to end in the worst scenario.

![linked-list](/algorithms/resources/linked-list.png)

![double-linked-list](/algorithms/resources/double-linked-list.png)

### FIFO

- `FIFO` (First In First Out): Queue (File [FR]): In this structure, the first element inserted is the first element removed.

It is possible to implement a Queue with a `static circular array` or a `linked list`.

![fifo](/algorithms/resources/fifo.png)

When a Queue is implemented with a `linked list`, it needs to maintain the following pointers:
- start (head of the queue)
- end (tail of the queue)

When we add an element in the queue, the end pointer is updated to the last element added.
When we remove an element from the queue, the start pointer is updated to the element that was pointed by the removed element.

![fifo-linked-list](/algorithms/resources/linked-list-queue.png)

### LIFO

- `LIFO` (Last In First Out): Stack (Pile [FR]): In this structure, the last element inserted is the first one removed.

In general, the following methods are used in a `stack`:
- `push()`: (empiler [FR]) add an element at the top of the stack
- `pop()`: (dépiler [FR]) remove and return the top element
- `peek()`: return the top element withtout removing it from the stack
- `isEmpty()`: return whether the stack is empty or not
- `size()`: return the number of element in the stack
- `clear()`: remove all elements in the stack

It is possible to implement a Stack with a `static array`, a `dynamic array` or a `linked list`.

![lifo](/algorithms/resources/lifo.png)

When a Stack is implemented with a `linked list`, it needs to maintain the following pointers:
- summit (latest element added)

When we add an element in the stack, the summit pointer is updated to the last element added.
When we remove an element from the queue, the summit pointer is updated to the element that was pointed by the removed element.

![lifo](/algorithms/resources/linked-list-lifo.png)

## Memoization

**Memoization** is the process of caching returned values of functions. This allows a program to lower its processing time.

In the example below, the results of `f(0)`, `f(1)`, `f(2)` and `f(3)` are memoized:

![memoization](/algorithms/resources/memoization.png)

## Bad Practices

1. Reallocating instead of emptying an already existent array

While it might seems a good idea to do:

```java
t = new int[size];
```

instead of:

```java
Arrays.fill(t, 0);
```

in fact, it is a very poor choice because for very big arrays, it will change the array pointer from the initial array to the new one. 

However, the old array will continue to exist until the Garbage Collector is woken up. So, for a humongous array, you'll take the risk of not having enough memory.

Generally, you'll simply have two arrays in memory whereas you can have only one. You use two times the space for a single array and you don't have the hand on when it will return to the normal situation.

![reallocating-instead-of-emptying](/algorithms/resources/reallocating-instead-of-emptying.png)

## Glossary

- `bulk operation`: refers to performing an operation on a large amount of data in a single request.
- `bulk data`: refers to putting all the data into a file or a set of files so that all of the data can be acquired with a few simple downloads.