# React

## Table of Contents

- [What is React](#what-is-react)
- [Principles of React](#principles-of-react)
- [JSX](#jsx)
- [React Basic Structure](#react-basic-structure)
- [React Imports and Exports](#react-imports-and-exports)
- [React Components](#react-components)
    - [Functional Components](#functional-components)
- [Modify CSS with React](#modify-css-with-react)

## What is React?

React is one of the most famous **JavaScript library**. It was created in 2011 by a Facebook software engineer. It became open-sourced in 2013. 

In 2015, **React Native** is released. It is dedicated to Android and iOS operating systems.

Please note that React **is not a framework** like Angular because it only manages the rendering layer. It does not take care of routing, queries...). It needs some other libraries to work completely.

## Principles of React

- React is `declarative`. The developer does not directly modify the **DOM** (**Document Object Model**). It is React which modify the Virtual DOM.

## JSX

React Components return a language which is similar to HTML but IT IS NOT HTML. So what can it be ??

It is the **JSX** language (**JavaScript XML**). It is JavaScript extension designed by React. It allows us to use tags directly with our JS variables. It is incredibly powerful because it is not empowered HTML, it is pure JavaScript.

So in order to manipulate data, we use JavaScript expressions. Theses expressions are always between brackets: `{ 6 * 7 }`

## React Basic Structure

## React Imports and Exports

## React Components

### Functional Components

A simple component
```js
function MyComponent() {
    return (<div>Hello OpenClassrooms 👋</div>)
}
```

Call a component
```js
<MyComponent />
```

## Modify CSS with React

The code below modifies the CSS of the given element. The style property takes an object in parameters so there is 2 pairs of brackets. The first one is the syntax of JSX and the second one is the declaration of an object in JS.
```js
<div className="my-element" style={{backgroundColor: isHovered ? "gray" : "white"}}>...</div>
```