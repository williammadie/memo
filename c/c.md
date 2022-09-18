# C Langage

## Table of Contents

- [Introduction](#introduction)
- [Advantages and Disadvantages of the C language](#advantages-and-disadvantages-of-the-c-language)
- [Compile and Run](#compile-and-run)
- [Basic Types in C](#basic-types-in-c)
- [Basic Libraries in C](#basic-libraries-in-c)
- [Structure of a C Project](#structure-of-a-c-project)
    - [Simple file project](#simple-file-project)
- [String Handling](#string-handling)
- [Inbuilt Typecast](#inbuilt-typecast)

## Introduction

The **C langage** is the direct evolution of the **B langage** created in 1969 by Kenneth Thompson. The **C langage** was born in 1972 alongside the development of *UNIX systems*. It was created by Kenneth Thompson and Dennis Ritchie. It is a basic language common to Windows, Linux and Mac Operating systems.

## Advantages and Disadvantages of the C language

|        **Advantages**       |           **Disadvantages**          |
|:---------------------------:|:------------------------------------:|
| Very powerful and efficient |       No implementation of OOP       |
|       Portable langage      |      Lack of exception handling      |
|     Middle level langage    |       Low level of abstraction       |
|      System Programming     |          Difficult to master         |
|    Allows memory handling   | Available libraries depend on the OS |

## Compile and Run

Compile a C file into an executable program
```bash
gcc file.c -o output-file-name
```

Compile and display all Warnings
```bash
gcc -Wall file.c -o output-file-name
```

Convert a C file into an Assembly file
```bash
gcc -S file.c
```

Run a C program
```bash
./output-file-name
```

## Basic Types in C

|  Type  |                               Description                              | Flag |
|:------:|:----------------------------------------------------------------------:|:----:|
|  char  |        Smaller machine unit. It can contains single characters.        |  %c  |
|   int  | Integer (values depends on processor) - bigger than or equals to short |  %d  |
|  short |                  Integer (values depends on processor)                 |  %i  |
|  long  |              Integer from -2 147 483 647 to 2 147 483 647              |  %ld |
|  float |                 Non-integer numbers (single precision)                 |  %f  |
| double |                 Non-integer numbers (double precision)                 |  %lf |

- *string* is not a basic type (it is a chain of *char*). However, it has its own flag: `%s`.

## Basic libraries in C

- *stdio.h* -> printf, scanf (for user input)
- *stdlib.h* -> memory allocation, basic constants (exit/success), conversions

## Structure of a C project

### Simple file project

```c
/*
Project: My_Project
Author: Author_Name
*/

#include <stdio.h>
#include <stdlib.h>

// Constant(s)

// Function Declaration(s)

int main(void) {
    return EXIT_SUCCESS;
}
```

## String handling

Check if 2 strings are equals
```c
strcmp(str1, str2)  // Returns a nonzero value if the strings are different and 0 if they're the same
```

## Inbuilt Typecast

Str -> int
```c
int a = atoi("9081222");
printf("%d\n", a);
// 9081222
```

Int -> Str
```c
int a = 90000;
int convertedStrLength = countDigits(a);
char* convertedStr = (char*)malloc((convertedStrLength+1)*sizeof(int));
sprintf(convertedStr, "%d", a);
convertedStr[convertedStrLength] = '\0';
printf("%s\n", convertedStr);
// 90000

//There is also the function itoa() but it is not part of the standard
```