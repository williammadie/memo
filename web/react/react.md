# React

## Table of Contents

- [Introduction](#introduction)
- [Start a React Project](#start-a-react-project)
    - [Prerequisite](#prerequisite)
    - [Use a toolchain](#use-a-toolchain)
- [React Basics](#react-basics)
    - [Project Structure](#project-structure)
    - [Package Management](#package-management)
    - [JSX](#jsx)
    - [Rules about Components](#rules-about-components)
    - [Historical Components](#historical-components)
    - [Functional Components](#functional-components)
    - [Virtual DOM and Rendering](#virtual-dom-and-rendering)
    - [States and Hooks](#states-and-hooks)
    - [Modify CSS with React](#modify-css-with-react)
- [Libraries of Components](#libraries-of-components)
- [Storybook](#storybook)

## Introduction

React is one of the most famous **JavaScript library**. It was created in 2011 by a Facebook software engineer. It became open-sourced in 2013. 

In 2015, **React Native** is released. It is dedicated to Android and iOS operating systems.

React has a **component-oriented architecture**. It is interesting for reusability.

Please note that React **is not a framework** like Angular because it only manages the UI and rendering layer. It does not take care of routing, queries... It needs some other libraries to work completely.

## Component Oriented Programming

### Pros

- reuse components
- easy way of documentating (doc as code, storybook)
- code more readable
- modularity
- component modification = recompilation of this component only

### Cons

- We must create a lot of components and anticipate our needs
- Software conception step is longer
- 

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

### Project Structure

```bash
my-react-project/
├── package.json            # Dependencies list
├── package-lock.json       # Lock versions of packages
├── README.md
├── node_modules/           # Project dependencies
├── public/                 # Generated website     
└── src/                    # Our project source folder
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js            # Main file of React (we'll never touch it)
    ├── logo.svg
    ├── reportWebVitals.js
    └── setupTests.js
```

### Package Management

- `"react": "^17.02",` => This version but you can choose the latest minor version
- `"react": "17.02",` => This version exactly

### JSX

React Components return a language which is similar to HTML but IT IS NOT HTML. So what can it be ??

It is the **JSX** language (**JavaScript XML**). It is JavaScript extension designed by React. It allows us to use tags directly with our JS variables. It is incredibly powerful because it is not empowered HTML, it is pure JavaScript.

So in order to manipulate data, we use JavaScript expressions. Theses expressions are always between brackets: `{ 6 * 7 }`

### Rules about Components

- 1 file = 1 component
- A component is not a class. It is a **function** (see next part).
- A component has a specific role.
- A component can be customized through its parameters.
- A component is always named in PascalCase.

### Historical Components

Historically, we used *classes* for our components. So, we could use OOP features (objects, constructors...)

However, now we don't use this approach anymore. We work with with functions only (*functional components*).

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

## Libraries of Components

- `React Router` => Routing/Navigation across the website
- `React hook form` => Handling forms (very complete but difficult to use)
- `Material UI` => Flexible and Pretty Buttons, Navbars...
- `Notification` => Sending notifications
- `Google Map` => Integration of a map

## Storybook

It is a way of documenting our application. It allows us to:

- focus on one component at a time
- segregate components so that they don't impact each others

Install Storybook
```bash
npx sb init
```

Launch Storybook
```bash
npm run storybook
```