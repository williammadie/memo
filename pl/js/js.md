# JavaScript

- [Data Types](#data-types)
- [Variables and Constants](#variables-and-constants)
- [Const, Var, Let](#const-var-let)
- [Asynchronous and Event Loop](#asynchronous-and-event-loop)
- [Handle Asynchronous Events](#handle-asynchronous-events)
- [Window, document and DOM](#window-document-and-dom)
- [String](#string)
- [Array](#array)
    - [Array Basic Operations](#array-basic-operations)
    - [Array Functions](#array-functions)
- [Functions](#functions)
- [Object and Class](#object-and-class)
- [Object Destructuring](#object-destructuring)
- [Operators](#operators)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Logical Operators](#logical-operators)
- [Variable Scope](#variable-scope)
- [Execute JS code](#execute-js-code)
- [Conditions](#conditions)
- [Loops](#loops)
- [Exceptions](#exceptions)
- [Functions](#functions)

## What is JavaScript

JavaScript is a **synchronous** programming language that can be used in `front`, `back`, `data science`. So it is usable everywhere. It is **weakly typed**.

For front-end development, it allows to **manipulate the DOM**.

By default, JS simulates **asynchronous behaviors** through its **event loop**.

It is made of a stack and a queue. 
- stack: the function being executed and heap of functions that need to be called
- queue: list of waiting events. They are processed when the stack is empty. 

In JS, everything is an **object**.

## API Calls

When we talk about API calls in JS, it is not necessarily a **network call**. It can be a call of JS to the **web browser** which is located on the user device.

## Data Types

JavaScript is a *weakly typed* and *monothreaded* (=> synchronous) programming language. There is no need to explicitely add the type of a variable when we declare it. (See in the below section).

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

## Const, Var, Let

- `let` => **block scope** and mutable
- `const` => **block scope** and immutable
- `var` => **global scope** and mutable (should never be used)

Reminder:
- **block scope** is delimited by `{}`
- **global scope** is dangerous because it defines a variable in the base object of a navigator which is **window**. In case of debugging, it would be a nightmare to find the error.

Always declare your variables as `const` if you don't think it is going to change. (Immutability = Performance)

## Asynchronous and Event Loop

How does JS can do asynchronous operation if it is single-threaded?

It uses an event-loop that simulates asynchronous behaviors:

```js
let x = 1;
const res = fetch();
x = 2
```

In this case, JS will process `x = 1`, then put the `fetch()` in a Queue and after that `x = 2`.

## Aysynchronous Behaviors

Asynchronous operations are used to interact with **APIs** that take time to respond:
- REST API: Network operations so it takes time before answering our call
- Web API: Browser/Dom

An API does not necessarily involve **network operations**.

Asynchronous behaviors are linked to **side effects** ([FR]: Effet de bord).

## Handle Asynchronous Events

**promise**: ?

### Fetch

First method for handling asynchronous operation:
A function that returns a promise
```js
const getCatFacts = async () => {
    return 'Cat fact';
}

getCatFacts().then((data) => console.log(data));
```

### Async / Await

Second method for handling asynchronous operation. It is just syntax sugar. In reality, it is rewritten as the first method internally.
```js
const getCatFacts = async () => {
    const response = await fetch(HTTP_URL);
    return response.json();
}
```

Important note: we don't `await` response.json() because it is not the responsability of the function to do so. It is the responsability of the calling function to await the result.

## Window, document and DOM

- `window` is the main object in JS
- `document` is contained inside window and allows te developer to access all **HTML nodes** (Document Object Model)

![window-document](/web/js/resources/window-document.jpg)

View of HTML Nodes (DOM):

![dom](/web/js/resources/dom.png)

In basic JS, we can acces DOM element by using `document.getElementById('myId')`

```html
<div id="myId">...</div>
```

We can then do different actions on this newly retrieved object:
- `addEventListener('click', functionToCall)`

The function `functionToCall` is called a **callback** (= a function that will be executed when there will be a click)

We can use a named function (like above) or an `anonymous function` (like below):

Event listener wiht Anonymous function
```js
document.getElementById("btn").addEventListener("click", function () {
    const square = document.getElementById("square");
    square.style.backgroundColor = `#${getRandomColor()}`;
});
```

## Prototypes

`prototype`: a blueprint for any object in JavaScript

By default, we can find `Object` and `Array` prototypes/blueprints.

For instance, all objects have the `myObject.__proto__` property. This property list all available object methods and properties.

![js-prototypes](/web/js/resources/js-prototypes.png)

## String

Observation: Both `"Hello!"` and `'Hello!'` are valid in JavaScript. The type of quotes you use is up to you. Find the one that fits best and stick to it.

Concatenate strings
```js
let name = "John";
name = name + " " + "Hammond";
```

(Most used way of concatenate string)
Concatenate strings (using string interpolation also called `string literals`)
```js
const batman = `Bruce Wayne`;
const sentence = `My name is ${batman}, I am Batman!`;
```

## Functions

Nowadays, JS developers mostly use the second way of declaring functions: 

1. Declare a named function
```js
function f1() {
    return ...;
}
```

2. Declare a lambda and store it into a variable
```js
const f1 = () => {...};
```

It takes less space. However, it is different from a classic named function.

=> A named function will be **defined for all the file**
=> A lambda stored in a variable **can't be used before it is defined**.

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

## Object Destructuring

We use this notation to get only keys in which we are interested
```js
// Returned object: {fact: "...", length: 12, isAlive: "true"}

function getHero() {
    return {
        name: 'Batman',
        realName: 'Bruce Wayne'
    }
}

const { name, realName } = await getCatFact();
console.log(`{name}, {realName}`);
```

## Array

### Array Basic Operations

Declare an Array
```js
const guests = ["Bruce Wayne", "Indiana Jones", "Peter Parker", "Tony Stark"];
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

### Array Functions

Array functions are:
- `find()` => find and return an element according to a function
- `filter()` => filter the array according to a function 
- `map()` => apply an operation for each array element
- `reduce()` => transform the array and return a single value according to a function (sum...)

Let's work on the following arrays:
```js
const notesInf1 = [3, 13, 18, 15, 10, 3];

const persons = [{firstName: "John", lastName: "Doe"}, {firstName: "Jane", lastName: "Doe"}];

```

Find first note equals to 10
```js
notesInf1.find(note => note === 10);
```

Get all notes different from 3
```js
const getAllNButThree = notesInf1.filter(note => note !== 3);
```

Convert the array of numbers to an array of objects that have the foloowing shape ({note: ..., coefficient: ...})
```js
notesInf1.map((note) => ({note: note, coefficient: note < 10 ? 1.5 : 3}));
```

Additional note on map object:
```js
// If we use the following notation, we MUST use the "return" keyword
notesInf1.map(note => {
    ...
    return myObject;
})
```

Another example of usage for the map function:
Add a field in an array of JSON objects
```js
persons.map(person => ({"firstName": person.firstName, "lastName": person.lastName, "fullName": `${person.firstName} ${person.lastName}`}));
```

A more optimized version would be:
```js
persons.map(({firstName, lastName}) => (
    firstName,
    lastName,
    fullName.`${person.firstName} ${person.lastName}`,
));
```

And a third alternative (not more optimized than the previous one):
```js
// Here we use the spread operator to decompose
// the fields of our object. If is equivalent
// to the previous solution
persons.map((person)) => (
    ...person,
    fullName.`${person.firstName} ${person.lastName}`,
);
```

Calculate the average as: `{'note': meanNote, 'coeff': meanCoeff}`
```js
// acc: final result at each step of the loop
// curr: current value in the loop
notesWithCoeff.reduce((acc, curr) => {
    acc.notes += curr.notes * curr.coeff,
    acc.coeff += curr.coeff,
    return acc
});

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

**Warning**: `var` is generally considered as a bad practice and most developers do not advice to use it. 

It was massively used before the introduction of `let` and `const` because there was no other way to declare a variable. However, a function scope variable can induce errors difficult to detect and so most languages use block scope variables. 

So in order to align onto these languages, please consider using `const` and `let` instead of `var`

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
function mean(arr) {
    let sum = 0;
    for (let el of arr) {
        sum += el;
    }
    return res / arr.length;
}
```

## JSON

**JSON**: **JavaScript Object Notation**

It is simply the notation for declaring an object in JavaScript.