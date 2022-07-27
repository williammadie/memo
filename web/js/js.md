# JavaScript

- [Data Types](#data-types)
- [Variables and Constants](#variables-and-constants)
- [String](#string)
- [Object and Class](#object-and-class)
- [Operators](#operators)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Logical Operators](#logical-operators)
- [Variable Scope](#variable-scope)
- [Execute JS code](#execute-js-code)
- [Conditions](#conditions)
- [Loops](#loops)
- [Exceptions](#exceptions)
- [Functions](#functions)

## Data Types

JavaScript is a *weakly typed* programming language. There is no need to explicitely add the type of a variable when we declare it. (See in the below section).

|  **Type** |             **Declaration**             |
|:---------:|:---------------------------------------:|
|   Number  |                let a = 42               |
|  Boolean  |              let b = false              |
|   String  |              let c = "John"             |
|    Null   |               let d = null              |
| Undefined |            let e = undefined            |
|   BigInt  | let f = BigInt(Number.MAX_SAFE_INTEGER) |
|   Object  |         let g = new Object1(...)        |

## Variables and Constants

In Javascript, variables and constants are named using *camelCase*

Declare a variable
```js
let myInt = 10;
let myFloat = 10.5;
let myString = "Hello!";
let boolean = true;
```

Declare a constant
```js
const myConstant = "Hello!";
```

## String

Observation: Both `"Hello!"` and `'Hello!'` are valid in JavaScript. The type of quotes you use is up to you. Find the one that fits best and stick to it.

Concatenate strings
```js
let name = "John";
name = name + " " + "Hammond";
```

Concatenate strings (using string interpolation)
```js
const batman = `Bruce Wayne`;
const sentence = `My name is ${batman}, I am Batman!`;
```

## Object and Class

*Reminder: A Class is a mold used to create several object of a same type*

Declare a simple object
```js
let sb1 = {
    modelName: "RF45LSQJF9249824",
    owner: "Indiana Jones",
    color: "Light Green"
};

console.log(sb1.title);

// OR

console.log(sb1["title"]);
```

Declare a simple class
```js
class SpeedBoat {
    constructor(modelName, owner, color) {
        this.modelName = modelName; // class property OR attribute
        this.owner = owner;
        this.color = color;
    }

    getModelName() {    // instance method
        return this.modelName;
    }
}

let sb2 = new SpeedBoat("RF45LK123OOI1", "John McCayne", "Night Blue");
sb2.getModelName();
```

Declare a class containing static methods
```js
class Utils {
    static removeAllFiles() {
        // Action
    }

    static connectToServer(ip) {
        // Action
        return //server instance
    }
}

Utils.removeAllFiles();
let server = Utils.connectToServer('127.0.0.1');
```

*Observation: All static methods could be simple functions but it is useful to create a static class because all these methods can be regrouped by type or usage*

## Array

Declare an Array
```js
let guests = ["Bruce Wayne", "Indiana Jones", "Peter Parker", "Tony Stark"];
```

Access the cell n°i of an Array
```js
guests[2]
// Peter Parker
```

Get the length of an Array
```js
guests.length
// 4
```

Add an element in an Array (at the end)
```js
guests.push("Harry Potter");
```

Add an element in an Array (at the beginning)
```js
guests.unshift("Harry Potter");
```

Delete the last element of the Array
```js
guests.pop();
```

## Operators

### Arithmetic Operators

| **Operator** | **Description** |
|:------------:|:---------------:|
|       +      |     addition    |
|       -      |   substraction  |
|       *      |  multiplication |
|       /      |     division    |
|      **      |   exponential   |
|       %      |     modulus     |

| **Operator** |        **Description**        |
|:------------:|:-----------------------------:|
|      +=      |    addition and assignment    |
|      -=      |  substraction and assignment  |
|      *=      | multiplication and assignment |
|      /=      |    division and assignment    |
|      %*      |     modulus and assignment    |
|      ++      |           increment           |
|      --      |           decrement           |

### Logical Operators

| **Operator** |    **Description**    |
|:------------:|:---------------------:|
|       <      |       less than       |
|      <=      | less than or equal to |
|       >      |       more than       |
|      >=      | more then or equal to |
|      ==      |        equal to       |
|      ===     |   strictly equal to   |
|      !=      |      not equal to     |
|      !==     | strictly not equal to |
|      !x      |         not x         |
|   x \|\| y   |         x or y        |
|    x && y    |        x and y        |

What is the difference between `a == b` and `a === b`?

Simple equal to
```js
if (5 == "5") {   // Checks if both values are equals BUT does not check if types are equals
    // Action1 (Here the condition is valid)
}
```

Strict equal to
```js
if (5 === "5") {    // Checks if both values are equals AND does check if types are equals
    // Action1 (Here the condition is not valid)
}
```

*Observation: The same specificity applies to `a != b` and `a !== b`*

## Variable Scope

In JavaScript, there are 3 keywords to declare a variable: `let`, `const` and `var`.

- `let` is a variable which has **block scope** (a block starts with `{` and ends with `}`)
- `const` is a constant which needs to be initialized when declared
- `var` is a variable which has a **function scope**

**Warning: `var` is generally considered as a bad practice and most developers do not advice to use it. It was massively used before the introduction of `let` and `const` because there was no other way to declare a variable. However, a function scope variable can induce errors difficult to detect and so most languages use block scope variables. So in order to align onto these languages, please consider using `const` and `let` instead of `var`**

## Execute JS code

In order to properly execute a JS script, you need to have the following structure:

```bash
project/
├── index.html
├── script.js
└── style.css
```

The main file is not the **.js** file, it is the **.html** one. It is in charge of importing the JS code and executing it.

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF8">
    <title>Page Web</title>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <p>Contenu de la page</p>
    <script src="./script.js"></script>
</body>
</html>
```

## Conditions

if
```js
if (condition) {
    // action1
} else if {
    // action2
} else {
    //default action
}
```

switch
```js
switch (variable) {
    case "value1":
        console.log("Action1");
        break;
    case "value2":
        console.log("Action2");
        break;
    default:
        console.log("Default Action");
}
```

## Loops

classic for loop
```js
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

for in loop (to iterate and use the index i)
```js
for (let i in passengers) {
    console.log("Boarding passenger " + passengers[i]);
}
```

for of loop (to iterate and not use the index i)
```js
for (let passenger of passengers) {
    console.log("Boarding passenger " + passenger);
}
```

classic while loop
```js
while (condition) {
    // Action1
    // Action2
}
```

## Exceptions

```js
try {
    // code that can throw an exception
} catch (error) {
    // Code to execute if error
}
```

## Functions

Declare a simple function
```js
function myFunction(p1, p2) {
    // do something
}
```