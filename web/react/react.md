# React

## Table of Contents

- [Introduction](#introduction)
- [Start a React Project](#start-a-react-project)
    - [Prerequisite](#prerequisite)
    - [Use a toolchain](#use-a-toolchain)
- [React Basics](#react-basics)
    - [JSX]
    - [Components]
    - [Virtual DOM and Rendering]
    - [States and Hooks]
    - [Modify CSS with React](#modify-css-with-react)

## Introduction

React is one of the most famous **JavaScript library**. It was created in 2011 by a Facebook software engineer. It became open-sourced in 2013. 

In 2015, **React Native** is released. It is dedicated to Android and iOS operating systems.

Please note that React **is not a framework** like Angular because it only manages the rendering layer. It does not take care of routing, queries...). It needs some other libraries to work completely.

## Start a React Project

### Prerequisite

React SPAs use `npm` (=**Node Package Manager**). It is an online repository for the publishing of open-source Node.js projects.

Install npm
```bash
sudo apt install npm
```

Check npm installation
```bash
npm -v
```

React SPAs also use `node`. Node is an open source development pltaform for executing JavaScript code server-side.

Install node
```bash
sudo apt install nodejs
```

Check node installation
```bash
node -v
```

### Use a toolchain

`Create React App` is a **toolchain** (=an environment for React). It is the best way to start building a new SPA in React:

Create and start a basic React App with NPX (=**NPM Script Environment/Utility**)
```bash
npx create-react-app my-app
cd my-app
npm start
```

## React Basics

### JSX

React Components return a language which is similar to HTML but IT IS NOT HTML. So what can it be ??

It is the **JSX** language (**JavaScript XML**). It is JavaScript extension designed by React. It allows us to use tags directly with our JS variables. It is incredibly powerful because it is not empowered HTML, it is pure JavaScript.

So in order to manipulate data, we use JavaScript expressions. Theses expressions are always between brackets: `{ 6 * 7 }`

### Components

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

### Virtual DOM and Rendering

### States and Hooks

## Modify CSS with React

The code below modifies the CSS of the given element. The style property takes an object in parameters so there is 2 pairs of brackets. The first one is the syntax of JSX and the second one is the declaration of an object in JS.
```js
<div className="my-element" style={{backgroundColor: isHovered ? "gray" : "white"}}>...</div>
```