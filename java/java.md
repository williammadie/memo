## Table of Contents

- [Introduction](#introduction)
- [Advantages and Disadvantages of the Java language](#advantages-and-disadvantages-of-the-java-language)
- [Basics](#basics)
    - [Compile and Run](#compile-and-run)
    - [Basic Types in Java](#basic-types-in-c)
    - [Basic Libraries in Java](#basic-libraries-in-c)
    - [Structure of a Java Project](#structure-of-a-c-project)
        - [Simple file project](#simple-file-project)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Arrays](#arrays)
    
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

- `Math`: (standard) it contains basic mathematical operations such as `abs(), pow(), log(), exp(), sin(), cos()`
- `System`: (standard) it allows the program to interact with the O.S (`System.out.println(), System.exit()`)

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

## Operators

|            Operator Name            |            Nom de l'opérateur           |                Symbols               |               Example               |                                                                  Comments                                                                 |
|:-----------------------------------:|:---------------------------------------:|:------------------------------------:|:-----------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------:|
|         Affectation Operator        |         Opérateur d'Affectation         |                   =                  |                a = 5;               |                                                                                                                                           |
|    Objects Construction Operator    |    Opérateur de Construction d'Objets   |                  new                 |        Car c1 = new Car(...);       |                                                                                                                                           |
|         Arithmetic Operators        |         Opérateurs Arithmétiques        |               + - * / %              |              a = 4 + 5;             |                                        These operators have the same priorities than in Mathematics                                       |
|      Unary Arithmetic Operators     |     Opérateurs Arithmétiques Unaires    |          ++a --a a++ a-- - +         |  for (int i = 0; i <= 6; i++) {...} |                                 These operators can be used as prefix or postfix (see full example below)                                 |
|    String Concatenation Operators   |  Opérateurs de Concaténation de Chaînes |                   +                  |   str1 = "Hello" + " " + "World!";  | This can be used but can induce the creation of a lot of objects. For this reason, it is generally advised to use the StringBuilder class |
|         Relational Operators        |         Opérateurs Relationnels         |            < > = != <= >=            |          if (a >= b) {...}          |  Beware while using these operators with objects : (a == b) for two objects will compare object's addresses and not the object on its own |
|          Logical Operators          |           Opérateurs Logiques           |               ! && \|\|              |    if (a && b \|\| c >= 6) {...}    |            If there are several conditions with \|\| and the first one is true, Java will not look at the following conditions            |
|           Ternary Operator          |            Opérateur Ternaire           |     expr ? trueValue : falseValue    |        a > b ? c = 1 : c = 0;       |                                          It can reduce a simple if/else to a one-line instruction                                         |
|        Typecasting Operators        |        Opérateurs de Transtypage        |    (int) (char) (String) (List)...   |             (int) 45.42;            |                                                      It can be used with all objects                                                      |
| Operation and Affectation Operators | Opérateurs d'Opération et d'Affectation | += -= *= /= %= &= ^= l= <<= >>= >>>= |               a += 4;               |                                             The last operators are used for binary operations                                             |
|            Comma Operator           |            Opérateur Virgule            |                   ,                  |       int a = 0, b = 1, c = 2;      |                                It is rarely used to declare and initialize several variables of a same type                               |
|          Bitwise Operators          |            Opérateurs Bitwise           |                ~ & ^ l               |                                     |                                                             Binary operations                                                             |
|           Shift Operators           |         Opérateurs de Décallage         |             >> << >>> <<<            |                                     |                                                             Binary operations                                                             |
|             Dot Operator            |             Opérateur Point             |                   .                  | c1.startEngine(); c1.remainingFuel; |                                    This operator is used to access methods and attributes of an object                                    |

For Unary Arithmetic Operators: 

Prefix Operators
```java
i = 0
j = ++i;

// equivalent to:

i = i + 1;
j = i;
// i = 1
// j = 1
```

Postfix Operators
```java
i = 0
j = i++;

// equivalent to:

j = i;
i = i + 1;
// i = 1
// j = 0
```

## Control Structures

IF/ELSE
```java
if (i % 2 == 0) {
  // Instructions
} else if (i > 0) {
  // Instructions
} else {
  // Instructions
}
```

RETURN (exit a function)
```java
return 9;
```

WHILE LOOP (if condition false = not entering the loop)
```java
while (i > 10) {  // Keeps running while it is true
  // Instructions
}
```

DO WHILE LOOP (if condition false = entering the loop one time)
```java
do {
  // Instructions
} while (i > 10); // Keeps running while it is true
```

FOR LOOP
```java
for (int i = 0; i <= 10; i++) { // Keeps running while i <= 10
  // Instructions
}
```

- The `break` keyword allows to leave/end a loop.
- The `continue` keyword allows to skip the end of the current iteration and to jump to the next iteration.

LOOP LABELS (allows to exit the main loop from inside the encapsulated loop)
```java
matrix:for (int i = 0; i <= 10; i++) {
  for (int j = 0; j <= 10; j++) {
    // Instructions
    break matrix;
  }
}
```

SWITCH CASE
```java
switch (value) {
  case "Value1":
    // Instructions
    break;
  case "Value2":
    // Instructions
    break;
  default:
    // Instructions
}
```

SWITCH CASE (with differents values resulting in the same action)
```java
switch (value) {
  case "Value1":
  case "Value2":
  case "Value3":
    // Instructions
    break;
  case "Value4":
    // Instructions
    break;
  default:
    // Instructions
}
```

## Arrays

Declaration
```java
int[] table;

//OR

int table[];
```

Initialization
```java
int[] table = {0, 1, 2, 3};

// OR

int[] table = new int[size_n] // An array length cannot be changed after it was initally set
```

Modify an Array
```java
table[2] = 15;
// {0, 1, 15, 3}
```

Access to elements of the array
```java
table[1];
// 1
```

Get the length of the array
```java
table.length
```

Loop on the array
```java
for (int value : table) {
  System.out.println(value);
}
```

Declare a multi-dimensional array
```java
int[][] table2D = new int[n][m];
```

Show the Memory Address of the Array
```java
System.out.println(table);
```

Show the values stored in the Array
```java
System.out.println(table.toString());
```

Check if two arrays are equals
```java
java.utils.Arrays.equals(arr1, arr2);
```

