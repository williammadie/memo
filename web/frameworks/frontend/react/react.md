# React

## Table of Contents

- [Introduction](#introduction)
- [Start a React Project](#start-a-react-project)
    - [Prerequisite](#prerequisite)
    - [Use a toolchain](#use-a-toolchain)
- [Project Structure](#project-structure)
- [Package Management](#package-management)
- [JSX](#jsx)
- [Rules about Components](#rules-about-components)
- [Historical Components](#historical-components)
- [Functional Components](#functional-components)
- [Virtual DOM and Rendering](#virtual-dom-and-rendering)
- [States and Hooks](#states-and-hooks)
    - [Custom Hook](#custom-hook)
    - [Effect Hook](#effect-hook)
- [Children Attributes](#children-attributes)
- [Context and Providers](#context-and-providers)
- [Modify CSS with React](#modify-css-with-react)
- [Libraries of Components](#libraries-of-components)
- [React Router Dom](#react-router-dom)
- [Storybook](#storybook)
    - [Create a Storybook file](#create-a-storybook-file)
- [Good Practices](#good-practices)
    - [High-Level Logic](#high-level-logic)

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

## Project Structure

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
    ├── components/         # All components
    ├── pages/  
    ├── hooks/              # All custom hooks
    ├── context/            # All ElementContext.js
    ├── logo.svg
    ├── reportWebVitals.js
    └── setupTests.js
```

## Package Management

- `"react": "^17.02",` => This version but you can choose the latest minor version
- `"react": "17.02",` => This version exactly

## JSX

React Components return a language which is similar to HTML but IT IS NOT HTML. So what can it be ?

It is the **JSX** language (**JavaScript XML**). It is JavaScript extension designed by React. It allows us to use tags directly with our JS variables. It is incredibly powerful because it is not empowered HTML, it is pure JavaScript.

So in order to manipulate data, we use JavaScript expressions. Theses expressions are always between brackets: `{ 6 * 7 }`

## What is a component?

**component**: is a function that returns HTML.

```jsx
import React from 'react';

const Text = ({ children }) => {
    return <p style={{textAlign: 'justify'}}>{children}</p>
}

// We use this instruction to export our component
// and be able to do:
// import Text from './Text';
export default Text;
```

## Rules about Components

- 1 file = 1 component
- A component is not a class. It is a **function** (see next part).
- A component has a specific role.
- A component can be customized through its parameters.
- A component is always named in PascalCase.

## Historical Components

Historically, we used *classes* for our components. So, we could use OOP features (objects, constructors...)

However, now we don't use this approach anymore. We work with with functions only (*functional components*).

## Functional Components

A simple component
```jsx
function MyComponent() {
    return (<div>Hello OpenClassrooms 👋</div>)
}

// or

const MyComponent = ({ firstname, backgroundColor }) => {
    return (
        <div style={{ backgroundColor: backgroundColor}}>
            Hello { firstname }!!
        </div>
    );
}

export default MyComponent;
```

Call a component
```js
<MyComponent />
```

## Component Lifecycle

- Montage du composant => Initialisation ou effet de bord
- Démontage du composant => Si un "nettoyage" du composant est requis à sa destruction
- Re-rendering du composant
    - Modification des props
    - Modification du state (Etat du composant)
    - Modification du composant parent

## Props and States

**properties**: are passed through the *parent component*

```jsx
const MyComponent = ({ prop1, prop2, propn }) => {
    ...
}
```

- state is handled inside the component (example: handle a date, a countdown)

## States Good Practices 

We can **use a state** when we want:
- to force the re-render of a component**
- calculate data
- we return HTML code through JSX

We don't use states when we want to simply store data. It will affect performance as the component will be re-rendered at each change even if it doesn't affect anything on it.

However, it is necessary to have a state if we display the value of the state in the HTML.

## States and Hooks

**hook**: helper function (e.g useState, useEffect...)

We can use a hook **to easily create and handle a state**. It is also possible to create custom hooks to handle some repetitive tasks.

Hooks always start by `use...()`

1. `useState()`: hook used to initialize and update a state.

```jsx
const [clicked, setClicked] = useState(false);
// clicked: variable that hold the state/the value
// setClicked: function used to update the state (we MUST use it for modifying a state)

return (
    <>
        <button
        onClick={() => setClicked(!clicked)}
        ...
        >
        </button>

        { clicked && (
            <span>Clicked!</span>
        )}
    </>
)

```

### Effect Hook

effect hook: a hook used to handle 2 parameters:
1. mount of a component
2. dismount of a component

We use the **effect hook** when we have to deal with side effects. ([FR] = effets de bord).

By default, `useEffect` is executed each time the component is re-rendered.

```js
useEffect(() => {
    fetchData();
})
```

We could use `useState` to query a resource. However, it would call the resource each time it is re-rendered.
```js
const [query, setQuery] = useState('query');

const fetchData = async () => {
    const result = await fetch(`https://...query=${query}`);
    setData(result.data);
}
```

However, if we add a parameter to `useEffect`, we can tell the function to query the resource only if the query element has changed.
```js
useEffect(() => {
    const fetchData = async () => {
        const result = await fetch(`https://...query=${query}`);

        setData(result.data);
    };

    fetchData();
}, [query]);    // <-- This parameter
```

**Important Note**: if we use an empty array in second parameter of `useEffect`, it will be called **only once** on the first mount.

### Custom Hook

A **custom hook** is a function that **itself uses a hook**.

It can be interesting in order to create a helper function to allow reusability at other places in our code.

```js
const useKanyQuote = () => {
    const fetchKanyeQuote = async () => {
        const result = await fetch(
            'https://api.kanye.rest/',
        );
    }
}
```

Use a custom hook:
```js
const fetchKanyeQuote = useKanyeQuote();
```

## Children Attributes

```js
const Title = ({children, size = "md"}) => {
    return (<h1 size={size}>{children}</h1>)
}

// children attribute refers to what is being passed between tags
<Title>Hello World!</Title>
```

## Context

The **context** is used **to share information across the application**. 

By default, we can only pass information from parents to children. However, with context, we can share information to any component we want!

How to use a context?

1. Create a context
2. Use and define a parent component
3. Provide context to components needing it

Defining SizeContext.js
```js
import { createContext } from react;

// 1 will be our default value
export const SizeContext = createContext(1);
```

Using SizeContext.js inside our component:
```js
const size = useContext(sizeContext);

... 

return {
    <Section>
        <SizeContext.Provider value = {size + 1}>
            { children }
        </SizeContext.Provider>
    </Section>
}
```

We could also imagine creating a context for handling `theme color`:
```js
import { createContext } from react;

// 1 will be our default value
export const ThemeContext = createContext("light");
```

example n°1: Passing the argument through component properties (without context)
```js
<Section>
    <Header size=1>Titre 1</Header>
    <Header size=1>Titre 2</Header>
    <Section>
        <Header size=1>Titre 3</Header>
        <Header size=1>Titre 4</Header>
    </Section>
</Section>
```

Pass the argument through component properties
```js
<Section>
    <Header size=1>Titre 1</Header>
    <Header size=1>Titre 2</Header>
    <Section>
        <Header size=1>Titre 3</Header>
        <Header size=1>Titre 4</Header>
    </Section>
</Section>
```

## Return several elements from a component

Use `<>` and `</>` (it is called a **fragment**)
```jsx
return (
    <>
        <button></button>
        <h1>Hello Guys</h1>
    </>
)
```

We can also put our `<button>` and `<h1>` inside a meaningful tag like `div` or `section`.

## Strange thing

It is possible to use this form instead of a traditional `if (loading)` in order to show an element
```jsx
loading && (
    <>
        <span>Merci de patienter</span>
        <span>Résultats dans un instant</span>
    </>
)
```

## Virtual DOM and Rendering

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

## React Router Dom

### Installation

This library allows React to handle routing and navigation between pages.

Install React Router Dom
```
npm install react-router-dom
```

Initially, your `index.js` should look like this:
```js
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

reportWebVitals();
```

In order to add React Router Dom, you have to modify it to the following one:
```js

```

### Usage

Navigate to another page 
```js
<Link to={constants.PATHS.ABOUT}>About Page</Link>
```

Method n°2: Navigate to another page
```js
const history = ...useHistory();

history.push(...)
```

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

### Create a storybook file

```jsx
import React from 'react';
import Card from './Card';

export default {
    component: Card,
    title: 'component/Card'
}

// Function to render to component in storybook
const Template = (args) => <Card {...args}>

// Default behavior of the component
export const Default = Template.bind();

Default.args = {
    title: '...',
    content: '...',
    textButton: '...',
    backgroundColor: '...'
}

// Behavior while loading
export const Loading = Template.bind();

Default.args = {
    title: '...',
    content: '...',
    textButton: '...',
    backgroundColor: '...'
}
```

## Good Practices

### High-Level Logic

In React, the code logic should be contained in a high-level **layouts** or **pages** not inside atomic component like buttons, labels...
