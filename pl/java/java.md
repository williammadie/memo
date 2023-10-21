## Table of Contents

- [Introduction](#introduction)
- [Advantages and Disadvantages of the Java language](#advantages-and-disadvantages-of-the-java-language)
- [Basics](#basics)
    - [Compile and Run](#compile-and-run)
    - [Dynamic Link and Classpath](#dynamic-link-and-classpath)
    - [Distributing a Java Program](#distributing-a-java-program)
    - [Good Practices and Interest Points](#good-practices-and-interest-points)
    - [Primitive Types in Java](#primitive-types-in-java)
    - [Object Type](#object-type)
    - [Wrapper Classes](#wrapper-classes)
    - [Implicit and Explicit Conversions](#implicit-and-explicit-conversions)
    - [Basic Libraries in Java](#basic-libraries-in-c)
    - [Structure of a Java Project](#structure-of-a-c-project)
        - [Simple file project](#simple-file-project)
- [Java Code Blocks](#java-code-blocks)
- [Comments and Java Conventions](#java-conventions-and-comments)
- [Operators](#operators)
- [String operations](#string-operations)
- [Control Structures](#control-structures)
- [Arrays](#arrays)
- [Collections](#collections)
  - [FIFO and LIFO Implementations](#fifo-and-lifo-implementations)
- [Classes](#classes)
	- [Structure of a file](#structure-of-a-file)
- [Handle null values](#handle-null-values)
    
## Introduction

Java was created in 1996 by Sun Microsystems. The company was then acquired by Oracle in 2010.

In 1996, the main goals of Java were:

- Allow developers to build software which would be independent from the hardware.
- Build an Object Oriented Programming language with wide standard libraries.


## Advantages and Disadvantages of the Java language

Java was primarily designed to support imperative programming (statements (=instructions) describe what the machine has to do step-by-step). So it is not a purely **Object-Oriented Language** because it is based on primitive types that aren't pure objects. However it supports major concepts of **Object Oriented Programming** (OOP).

A quick view of the different programming paradigms:

| Paradigm Name                  | Nom du Paradigme                   | Description                                                                                                                       | Other paradigm engulfed |
|--------------------------------|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| Imperative Programming         | Programmation Impérative           | The entire program is a single algorithm which complete a functionality written step by step. (No function, No module, No object) |                         |
| Structured/Modular Programming | Programmation Structurée/Modulaire | Most often these two terms can refer to a same paradigm: program is divided into units of work which can be functions or modules. | Procedural Programming  |
| Object-Oriented Programming    | Programmation Orientée Objets      | The program is divided in classes, object and links between objects.                                                              |                         |

A quick recap on why OOP is the world most popular programming paradigm:

![structured-programming-vs-oop](/programming_languages/java/resources/structured-programming-vs-oop.jpg)

## Basics

### Compile and Run

Java is independent from the computer it is running on. This is achieved with the **JVM (Java Virtual Machine)**: the code produced by the **JDK (Java Compiler)** is known as bytecode. This bytecode is a known language of the JVM.


Basic steps to run a Java Program:

1. Use the JDK to compile the source code into bytecode (file.java -> file.class)
2. Use the JVM to run this bytecode file (file.class)


![java-compile-and-run](/programming_languages/java/resources/java-compiler-and-execution.png)


Java Architecture in a nutshell:

![java-architecture](/programming_languages/java/resources/java-architecture.png)

As we can see, the JDK contains a JRE that contains the JVM. Developers will use the JDK where users will only use the JRE containing the JVM.


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

Note: the **JRE (Java Runtime Environment)** is different from the **JVM (Java Virtual Machine)** (the JVM is contained in the JRE):

- JRE = JVM (tools to run Java programs)
- JDK = JSHELL + JVM + JRE + ... (tools to develop a Java program).

Nowadays, we can find different version of the Java source code. The one maintained by Oracle is called **OpenJDK**.

### Dynamic Link and Classpath

A Java program is a group of .class files (compiled files). Even if our program is very basic we're still dependent from the System class which is contained in the Standard library (= a bunch of .class files).

In a complex program, there can be libraries located at different places in the system. For this reason, we can use the argument `-classpath library-locatio` while running a java program.

Specify a library location to a Java program
```bash
java -classpath /home/william/... myProgram

// OR

export CLASSPATH=/home/william/...
java myProgram
```

### Distributing a Java Program

As said previously, a Java program is a collection of .class files. It looks difficult to distribute a folder filled with thousands of .class files to our client. So how can we proceed ?

To distribute our program at an important scale, we'll use **JAR files** (= **Java ARchive**) which are basically a ZIP file containing .class files. It looks like this: `myExecutable.jar`

Create a JAR:
```bash
jar -cf Cycle.jar cycle.class 
```

Add a JAR to CLASSPATH to use all contained files
```bash
export CLASSPATH=/home/william/...
java MyProgram
```

**All Java libraries are available under the JAR format.**

### Good Practices and Interest Points

- There is maximum 1 class per file.
- The file should be named after the class it contains.
- 1 line should contain 1 instruction (instructions are separated by `;`).
- one-line comment: `//`
- multi-line comment: `/*`
- javadoc: `/**`
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

### Wrapper Classes

In Java, everything is based on Object handling. Most of the methods only accepts Objects and not primitive types.

For instance, if I want to create a set in Java I will use the Collections.Set which only handle Objects. So how can I do ?

You have to wrap your primitive value in an Object by using **Wrapper Class**. They are different classes for all primitive values:

![wrapper-classes](/programming_languages/java/resources/wrapper-classes-java.png)

```java
Set<int> mySet = new HashSet<>();   // Not valid because Set expects an Object not a primitive value

Set<Integer> mySet = new HashSet<>();   // Valid because Integer is a Wrapper Class, so it is not primitive anymore
```

Note: Java also support **Autoboxing** which refers to the *implicit cast (see part below)* of a **primitive value** to a **Wrapper Class**.

Autoboxing of a primitive value
```java
Integer i = 89;

// We don't need to do:
// (although it is possible)
Integer i = Integer.valueOf(89);

// In the other way we must explicit the cast:
int k = i.intValue();
```

### Implicit and Explicit Conversions

In Java, there is two types of conversions for primitive types:

- Widening/Implicit Conversion (Safe Conversion): it is handled automatically by Java.
- Narrowing/Explicit Conversion (Unsafe Conversion): it is handled by the developer and has a chance of failure. 

The image below shows these two types of conversions

![typecasting-java](/programming_languages/java/resources/typecasting-in-java.jpg)

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

## Java Code Blocks

Java use `{...}` to delimit a code block. A *code block* is used to limit the scope of a variable.

```java
int a = 34;
{
  int b = 35;
}
System.out.println(a);
// 34
System.out.println(b);
// Error: b is not defined
```

A code block can be used after a *if* to highlight a condition:

```java
if (a >= 10) {
  // Instructions
}
```

It can also be an *anonymous code block* which refers to a code block where it is not required. Please note that using such block can be a sign that our code needs to be refactored. In the case below, it helps to structure a declaration of UI elements in Swing

```java
JPanel mainPanel = new JPanel(new BorderLayout());
{
    JLabel centerLabel = new JLabel();
    centerLabel.setText("Hello World");
    mainPanel.add(centerLabel, BorderLayout.CENTER);
}
{
    JPanel southPanel = new JPanel(new FlowLayout(FlowLayout.LEFT, 0,0));
    {
        JLabel label1 = new JLabel();
        label1.setText("Hello");
        southPanel.add(label1);
    }
    {
        JLabel label2 = new JLabel();
        label2.setText("World");
        southPanel.add(label2);
    }
    mainPanel.add(southPanel, BorderLayout.SOUTH);
}
```

## Comments and Java Conventions

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

## String operations

Get String length
```java
String str = "Hello World!";
str.length();
```

Check if a String is empty
```java
str.isEmpty();
```

Get the character at a given index
```java
str.charAt(4);
// o
```

Get the first index of a character
```java
str.indexOf('o'); // returns -1 if not found
// 4
```

Get the first index of a character after a given index
```java
str.indexOf('o', 5);
// 7
```

Get the first position of a substring in the String
```java
str.indexOf("World"); // Case sensitive!
// 6
```

Get the first position of a substring in the string after a given index
```java
str.indexOf("World", 4);
// 6
```

**There is function that works in a similar way. It is called `lastIndexOf(...)`. It allows to find the last index of a character or a substring**

Compare Two Strings - Case sensitive
```java
"alban".compareTo("boris");
// -1 (lexicographic order)

"alban".compareTo("alban");
// 0 (Strictly equals)

"boris".compareTo("boris");
// 1  (lexicographic order)
```

Compare Two Strings - Cases insensitive
```java
"ALBAN".compareToIgnoreCase("boris");
// -1
```

Changing Case
```java
str.toLowerCase();
// hello world!

str.toUpperCase();
// HELLO WORLD!
```

Removing Trailing Whitespace
```java
String str2 = "     Hi guys, I'm Marc!     ";
str.trim();
// "Hi guys, I'm Marc!"
```

Format Strings
```java
String.format("I'm %d years old", 19);  // Useful for printing
// I'm 19 years old
```

Flags for formating Strings:

- `%d` for byte, short, int, long, BigInteger
- `%s` for Strings
- `%f` for float, double as a decimal number
- `%e` for float, double as a decimal number in scientific notation
- `%b` for boolean

For floating numbers, it is also possible to specify a **precision** which is basically the number of digits we want to show after the comma.

Format Strings with precision
```java
double ourDouble = 1123.9303;
String.format("%f", ourDouble);
// 1123.9303
String.format("%.3f", ourDouble);
// 1123.930
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

Copy an array
```java
int[] arr1 = {1, 2, 3, 4, 5};
int[] arr2 = Arrays.copyOf(arr1, arr1.length);
// arr2 = [1, 2, 3, 4, 5]
```

## Collections

### FIFO and LIFO Implementations

Both structures can be implemented by using an `ArrayDeque` which is an **Array Double Ended Queue**. This means that in this array, we can add or remove an element from both sides. The only difference between a `FIFO` and a `LIFO` structure implementation will be the associated interface.

**FIFO Implementation**
```java
Queue<String> myQueue = new ArrayDeque<String>();
```

FIFO Methods:
- `offer(E element)`: Insert the specified element inside the queue
- `peek()`: Retrieve but does not remove the head of the queue
- `poll()`: Retrieve and remove the head of the queue
- `clear()`: Remove all elements from the queue
- `isEmpty()`: Check if the given queue is empty or not

**LIFO Implementation**
```java
Deque<String> myStack = new ArrayDeque<String>();
```

LIFO Methods:
- `push(E element)`: Push an element onto the stack
- `peek()`: Retrieve the element on top of the stack without removing it
- `pop()`: Retrieve the element on top of the stack and remove it
- `clear()`: Remove all elements from the stack
- `isEmpty()`: Check if the given stack is empty or not

## Classes

### Structure of a class

```java

public class SeaPlane extends Plane {		// a sea plane is a plane so it inherits of its attributes (and methods)
	
	// Static Variable (= ALL sea planes are restricted to go higher than this speed limit)
	// It is initialized on declaration
	private static int maximalAuthorizedByLawSpeed = 500
	// Instance Variable (= EACH sea plane has its own type of VIP services)
	// It is initialized via the Constructor after declaration 
	private ArrayList<VipService> vipServices;			
	
	// Constructor of a SeaPlane object/instance
	public SeaPlane(Model model, Category category, ArrayList<VipServices> vipServices) {
		super(model, category);
		this.vipServices = vipServices;
	}
	
	public ArrayList<VipService> getVipServices() {
		return this.vipServices;
	}
	
	public void setVipServices(ArrayList<VipService> vipServices) {
		this.vipServices = vipServices;
	}

  // A public method which does something. It includes a call to a private function
  // that only sea planes can use. 
  public void doSomething(...) {
    ...
    doSomethingThatOnlyYourTypeCanDo();
    ...
  }

  // A private method that can be used only in this class/file. Only sea planes objects can
  // call this method (access modifier: private)
  private void doSomethingThatOnlyYourTypeCanDo() {
    ...
    ...
    ...
  }
}
```

Note: public, private, protected and default are called access modifiers

## Handle null values

In Java, there is a better way of handling null values especially when these values are returned by functions. It goes through the use of the `Optional` java feature.

A function can return `an object` or an `Empty Optional`. 