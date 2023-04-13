# The Dart Language

## Table of Content

- [Introduction](#introduction)
- [Dart Major Principles](#dart-major-principles)
- [Minimal Dart Application](#minimal-dart-application)
- [Built in data types](#built-in-data-types)
- [Operators](#operators)
- [Collections](#collections)
- [Control Flow Statements](#control-flow-statements)
- [Functions](#functions)

## Introduction

Dart 1.0 was released by Google in 2013. It aims at building mobile (with Flutter), desktop and modern web applications from a single code base.

## Dart Major Principles

- Dart is **clean, simple and class-based**
- Dart is a **pure object-oriented programming language** (everything is an object)
- Dart was initally **designed to be compatible with the web**. It comes up with a JavaScript compiler which translates Dart source code to JavaScript
- Dart works with an **Ahead Of Time (AOT)** compiler. It compiles to fast, predictable, native code. 
- Dart is **an imperative language** (instructions are executed in a sequential order, fromt top to bottom)
- Dart is **strongly-typed** (variable types need to be declared before variables are used)

## Minimal Dart Application

```dart
void main() {
    print("hello world!");
}
```

Non web application reading input
```dart
// Support for non-web application
import 'dart:io';

void main() {
  // To handle null safety, we use "?"
  String? myInput = stdin.readLineSync();
  print('Hello $myInput!');
}
```

## Built in data types

In Dart, even primitive types are objects. This means that everything use **reference type**. For instance, an unitialized variable has the value of `null`.

- Number
- String
- Boolean
- List
- Set
- Map
- Rune
- Symbol

### Number

There are three main types:

- `num` (mother categorie. It includes both `int` and `double`)
- `int`
- `double`

### String

- `String`
- We can use `"` or `'` for **String Literals** (ex `"Hello"`)
- Concatenation: `s1 + s2`
- String Interpolaton: `"Hello $name" or "Hello ${27+3}"`
- Mutliple lines: 

```dart
String s1 = "Hello"
    " World!"
    " I'm gonna destroy everything!";

// or

String s1 = """Hello
World!
I'm gonna destroy everything!""";
```

### Boolean

- `bool`
- `true` or `false`
- defining a boolean without initialization gives `null`

### Type Inference and Dynamic Types

Dart is able to declare a variable without explicitly mentioning the data type:

```dart
// Authorized
var myVariable = 12;

// or

num myVariable = 12;
```

But in this case, how to know the type of an object?

Show the type of an object
```dart
print(myVariable.runtimeType);
```

It is also possible to use a dynamic typed variable:
```dart
dynamic myVar = "A String";  //String

myVar = 4;  // int

myVar = true;   // bool
```

### Constant

Two possible ways:
- at runtime or compiletime: `final`
- at compiletime `const`

## Operators

|        **Operator Name**       |          **Symbols**          |      **Example**      |                             **Comments**                            |
|:------------------------------:|:-----------------------------:|:---------------------:|:-------------------------------------------------------------------:|
|      Affectation Operator      |               =               |                       |                                                                     |
| Assignment Operators           |     += -= *= /= %= &= ~/=     |                       |                                                                     |
|      Arithmetic Operators      |          + - * / % ~/         |       5 ~/ 2 = 2      |                      "~/" is a integer division                     |
|   Unary Arithmetic Operators   |      ++a --a a++ a-- - +      |          i++          |                                                                     |
| String Concatenation Operators |               +               |                       |                                                                     |
|      Relational Operators      |        < > == != <= >=        | if (myVar == "hello") |                                                                     |
|        Logical Operators       |           ! && \|\|           |     if (a \|\| b)     |                                                                     |
|        Ternary Operator        | expr ? trueValue : falseValue |                       |                                                                     |
|      Type Testing Operator     |             is is!            |  if (myVar is! bool)  |                  The is! corresponds to a "is not"                  |
|      Typecasting Operator      |               as              |                       |                                                                     |
|        Bitwise Operators       |            ~ & ^ \|           |                       |                                                                     |
|         Shift Operators        |             >> <<             |      5 << 2 = 20      | The bits of the left operand are shifted by 2 bits towards the left |

## Collections

### List

Create a empty list
```dart
var myList = List<String>();
```

Create a list with values
```dart
// Here type is inferred to List<int>
var myList = [780, -13, 2, 3, 31];
```

Access an element
```dart
print(myList[0]);
// 780
```

Get the length
```dart
myList.length;
```

Add an element
```dart
myList.add(4);
```

Add a list of elements
```dart
myList.addAll(mySecondList);
```

Remove an element
```dart
myList.removeAt(1);
```

Find index of an element
```dart
myList.indexOf(-13);
```

Clear the list
```dart
myList.clear();
```

Apply an operation to all elements
```dart
var myList = [780, -13, 2, 3, 31];
var myMappedList = myList.map((e) => e * 100).toList();
```

Filter a list
```dart
var evenList = myList.where((e) => e % 2 == 0).toList();
```

### Set

Create an empty set
```dart
var mySet = <int>{};
// or
Set<int> mySet = {};
```

Create a set with values
```dart
var mySet = {1, 23, 56};
```

Add an element
```dart
mySet.add(3);
```

Add a set of elements
```dart
mySet.addAll(mySecondSet);
```

Get the length
```dart
mySet.length;
```

Remove an element
```dart
mySet.remove(56)
```

Check if an element belong to a set
```dart
mySet.contains(23);
```

Set Operation: Include
```dart
mySet.containsAll(anotherSet);
```

Set Operation: Intersection
```dart
mySet.intersection(secondSet);
```

Set Operation: Union
```dart
mySet.union(mySecondSet);
```

### Map

Create an empty map
```dart
var myMap = Map<int, String>();
```

Create a map with value
```dart
var myMap = {
  "France": "Paris",
  "United Kingdom": "London",
  "Germany": "Berlin",
  "Italy": "Rome"
};
```

Add an element
```dart
myMap[key] = newValue;
```

Get the length
```dart
myMap.length;
```

Access a value
```dart
// It returns "null" if the key doesn't exist
myMap[key]
```

Check if a key exists
```dart
myMap.containsKey(myKey);
```

Get all the keys
```dart
myMap.keys;
```

Get all the values
```dart
myMap.values;
```

Remove a couple (key: value)
```dart
myMap.remove(key);
```

## Control Flow Statements

If else
```dart
if (condition1) {
  // Action1
} else if (condition2) {
  // Action2
} else {
  // Action3
}
```

For Loop
```dart
for (var i = 0; i < 10; i++) {
  print(i);
}
```

Foreach Loop
```dart
for (var color in colors) {
  print(color);
}
```

While Loop
```dart
while (i <= 10) {
  // Action
}
```

Do While Loop
```dart
do {
  // Action
} while (i <= 10);
```

Infinite Loop
```dart
while (true) {
  // Action
}

// or

for (;;) {
  // Action
}
```

Note: In Dart, the keywords `break` and `continue` can be used in loops.

```dart
switch (result) {
  case value1:
    // Action1
    break;
  case value2:
    // Action2
    break;
  default:
    // Default Action
}
```

Throw an exception
```dart
// Assert throws an exception if a condition is false
assert(conditionToEvaluate);
```

## Functions

```dart
void myFunction(num x, String y) {
  // Actions
}
```

### Shorthand Function

Write a shorthand function 
```dart
// The "num" at the left is the return type of the function
num sum(num x, num y) => x + y;
```

Dart also handles optional parameters. We can use them like this:

Optional Named Parameters
```dart
void doSomething(num p1, {String p2, num p3}) {
  // If p2 or p3 is not given, it will simply print "null"
  print(p1);
  print(p2);
  print(p3);
}

// Call
doSomething(5, p2: "Hello!");
```

Optional Positional Parameters
```dart
void doSomething(num p1, [String p2, num p3]) {
  // If p2 or p3 is not given, it will simply print "null"
  print(p1);
  print(p2);
  print(p3);
}

// Call
doSomething(5, "Hello!");
```
**Note**: With positional parameters we are forced to follow the parameters' declaration order. So we cannot give p3 if p2 is not given.

### Higher-order Function

In Dart, everything is an object. It even applies to functions. So it is completely possible to pass a function as a parameter or to return a function. A function that take other functions as parameters or that return functions as results is called **higher-order functions**.

Higher-order function
```dart
// This function applies the f function to each element of a given list. Then, it adds the new element to a new list
// and returns this new list
List<int> myHighOrderFunction(Function f, List<int> myList) {
  var newList = List<int>();
  for (var i = 0; i < myList.length; i++) {
    newList.add(f(myList[i]));
  }
  return newList;
}
```

Dart has a similar builtin function:
```dart
// The function we pass to forEach must return nothing (void)
var myList = [1, 2, 3, 4];
myList.forEach(print);
```

### Anonymous Function

Anonymous Function/Lambda/Closure refers to the same concept.

Anonymous Function
```dart
// It looks like this
(parameters) {
  // Action
}


myList.forEach((item) {
  print(item*item*item)
})
```

### Nested Function

This refers to a function defined inside another function.

Nested Function
```dart
void outerFunction() {
  void nestedFunction() {
    // Do something
  }
}
```

An example
```dart
int max(int a, int b, int c) {
  int max(int a, int b) {
    return a > b ? a : b;
  }
}
```

## Scope

In Dart, the scope of variables is limited to `{}` (as in Java)

## Class

Define a class
```dart
class Person{
  String name;    // Unitialized: value = null
  String gender;  // Unitialized: value = null
  int age;

  Person(String name, String gender, int age) {
    this.name = name;
    this.gender = gender;
    this.age = age;
  }

  // It is possible to remove the body of the constructor if parameters have the same names as attributes
  Person(String name, String gender, int age);

  // It is also possible to write several constructors. In this case we can name them:
  Person.newBorn() {
    this.age = 0;
  }

  // Getter function
  String get getName => name;

  // Setter function
  void set setName(String name) {
    this.name = name;
  }

  walking() => print("$name is walking");   // Instance method
}
```

Instantiate a class
```dart
var p1 = Person();
```

Use an instance variable (=attribute) or an instance method
```dart
p1.gender;
p1.walking();
```

## Inheritance

```dart
class Car extends Vehicle {
  String _model;
  num _noSerial;

  Car (String _model, num _noSerial) : super(name, price, kilometers);
}
```
**Note**: A method or a variable starting with `_` is private. It cannot be used in daughter classes.