# Angular

## Create a new Project

First, you have to know that you can't have **more than one** angular project active at the same time. If you already have another angular project, you'll have to delete the *~/.npm* folder. If you don't do so, the **ng new** command will fail. 

## Main commands

Create a new Angular Project
```bash
ng new nom_projet
```

Launch the Web Development Server
```bash
ng serve --open
```

Create a new Component
```bash
ng generate component my-component
```
(Each hyphen will add a capital letter on the following letter)

In order to use the Component in the *app.component.html*, you have to use a special HTML tag named after your component:

```html
<app-my-component></app-my-component>   <!-- Instance n°1-->
<app-my-component></app-my-component>   <!-- Instance n°2-->
<app-my-component></app-my-component>   <!-- Instance n°3-->
<app-my-component></app-my-component>   <!-- Instance n°4-->
```
(Don't forget to prefix the tag with *app-*)

This tag will create one instance of the component "app-my-component". ***Each component is independent*** so if we modify the value of an attribute on the first component, the other instances **will not be affected**.

## Known errors

```bash
ng generate component nom-component
```

**Could not find an NgModule. Use the skip-import option to skip importing in NgModule.**

### Quick fix

- If *app.module.ts* is not present, create it in *src/app/*
- Make sure to execute the `ng generate` in the *src/app/* folder