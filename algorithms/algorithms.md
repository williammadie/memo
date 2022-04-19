# Algorithms

## Table of Contents

- [Algorithm Complexity](#algorithm-complexity)
    - [Introduction](#introduction)
    - [Big O Notation](#big-o-notation)
    - [Different types of Complexity](#different-types-of-complexity)
    - [Cheat Sheet](#cheat-sheet)
- [Sorting Algorithms](#sorting-algorithms)
    - [Insertion Sort](#insertion-sort)

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

![img1](/algorithm/resources/complexity-explained.png)

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

![img2](/algorithm/resources/complexity-graph.png)

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