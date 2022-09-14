## Table of Contents

- [Introduction](#introduction)
- [Advantages and Disadvantages of the Java language](#advantages-and-disadvantages-of-the-java-language)
- [Basics](#basics)
    - [Compile and Run](#compile-and-run)
    - [Basic Types in Java](#basic-types-in-c)
    - [Basic Libraries in Java](#basic-libraries-in-c)
    - [Structure of a Java Project](#structure-of-a-c-project)
        - [Simple file project](#simple-file-project)
    
## Introduction


## Advantages and Disadvantages of the Java language

## Basics

### Compile and Run

Basic steps to run a Java Program:

![java-compile-and-run](/java/resources/java-compiler-and-execution.png)


Compile a *Java Source Code* file into a *Java Byte Code file*
```bash
javac JavaFilename.java
```

Run a *Java Byte Code file*
```bash
java JavaFilename
```

Compile and Run as a script
```bash
java JavaFilename.java
```

### Good Practices and Interest Points

- There is maximum 1 class per file.
- The file should be named after the class it contains.
- 1 line should contain 1 instruction (instructions are separated by `;`).
- one-line comment: `//`
- multi-line comment: `/*`
- javadoc: `/*`
- classes should be named using *PascalCase*.
- variables should be named using *camelCase*.
- methods (= functions inside classes) should be named using *camelCase*.
- constants should be named like *MAX_WIDTH*.
- packages should be named using a reversed website name: *fr.pantheonsorbonne.miage* where each part of the name like *fr*, *pantheonsorbonne* and *miage* is a subfolder of the previous folder. (see illustration below).

```bash
fr
└── pantheonsorbonne 
        └── miage   
```

### Primitive Types in Java

Primitive types are types of variables that can use arithmetical operations (or logical in the case of the boolean).

|   Type  |                                      Description                                      |                Definition Domain               |   Size  |       Example       |
|:-------:|:-------------------------------------------------------------------------------------:|:----------------------------------------------:|:-------:|:-------------------:|
| boolean |                         Logical values: 0 or 1 (true or false)                        |                  true / false                  |  1 bit  |         true        |
|   char  |                                   A single character                                  |                   ASCII Table                  | 16 bits |         'b'         |
|   byte  |                            Integer with a very tight range                            |                 [ -128 ; 127 ]                 |  8 bits |          5          |
|  short  |                               Integer with a tight range                              |               [ -32768 ; 32767 ]               | 16 bits |        -24567       |
|   int   |                              Integer with a normal range                              |           [-2147483648 ; 2147483647]           | 32 bits |      2147483647     |
|   long  |                             Integer with a very wide range                            | [ -9223372036854775808 ; 9223372036854775807 ] | 64 bits | -922337203685470000 |
|  float  |   Floating number with a normal range (single precision: 6 numbers after the comma)   |           [ 1.4E-45 ; 3.4028235E38 ]           | 32 bits |       2.3E-23       |
|  double | Floating number with a very wide range (double precision: 15 numbers after the comma) |      [4.9E-324 ; 1.7976931348623157E308 ]      | 64 bits |       4.2E-245      |

Note that:
- operations involving *byte, short, int, long* will give an exact result if values are in their corresponding range. 
- operations involving *float and double* will give an approximate result if values are in their corresponding range.

The only way to compare values with float and double is to use something like :
```java
Math.abs(4,14 - (3,14+1)) < 0,0001 // where 0,0001 is called the Machine Epsilon
```

The **Machine Epsilon** is a system constant that gives the precision of a CPU. It is not the same on each machine.

### Object Type

Objects are everything else in Java : it refers to types that aren't primitive. An object has **attributes/properties** and **methods** (=functions inside of a class).

### Implicit and Explicit Conversions

In Java, there is two types of conversions for primitive types:

- Widening/Implicit Conversion (Safe Conversion): it is handled automatically by Java.
- Narrowing/Explicit Conversion (Unsafe Conversion): it is handled by the developer and has a chance of failure. 

The image below shows these two types of conversions

![typecasting-java](/java/resources/typecasting-in-java.jpg)

Note that a *narrowing/explicit* conversion can be forced by using `(int)variable OR (float)variable OR ...`.

### Basic Libraries in Java

### Structure of a Java Project

#### Simple file Project

A single file project will contain at least:

```java
public class FirtProgram {

  public static void main(String[] args) {
    System.out.println("Hello World!");
  }

}
```

The file will be **named after its class**: ``FirstProgram.java`.