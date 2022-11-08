# Programming Languages

## Table of contents

- [Type Systems](#type-systems)
    - [Static VS Dynamic Typing](#static-vs-dynamic-typing)
    - [Strong VS Weak Typing](#strong-vs-weak-typing)

## Type Systems

**type system** refers to a **logical system comprising a set of rules that assigns a property called a type to every variable**

Two concepts of **system typing** are commonly confused: 
- Static/Dynamic Typing => **When** is type information acquired?
- Strong/Weak Typing => **How strictly** types are distinguished? (Are implicit conversion authorized?)

### Static VS Dynamic Typing

In a **statically typed language**, type is determined at compile time so a variable cannot change its type after it is declared. (typing is associated with **the variable**)

For instance, Java is statically typed:
```java
String v1 = "hello";
v1 = 5;
// Error : not possible
```

In a **dynamically typed language**, type is determined at runtime so a variable can change its type at any moment. (typing is associated with **the value** of a variable)

For instance, Python is dynamically typed:
```python
>>> v1 = "hello"
>>> v1 = 5
# No problem
```

### Strong VS Weak Typing

**Please note** that many professional developers **avoid these two terms** because they don't have a **universally agreed on technical meaning**.

Commonly agreed:

In a **strongly typed language**, type matters when performing operations on a variable. Thus, implicit conversions are not authorized.

For instance, Python is strongly typed:
```python
>>> 5 + "hello"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

In a **weakly typed language**, type doesn't matter when performing operations on a variable. Thus, implicit conversions are authorized.

For instance, PHP is weakly typed: (it is a very forgiving language!)
```php
$str = 5 + "hello";
// This equals 5 because "hello" is implicitely casted to 0
```