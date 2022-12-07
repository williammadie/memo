# Angular

## Table of Content

- [Installation](#installation)
    - [Prerequisites]
    - [Install Angular](#install-angular)
    - [Modify Environment](#modify-environment)
- [Create a new Project](#create-a-new-project)
    - [Main commands](#main-commands)
    - [Known errors](#known-errors)
    - [Quick fix](#quick-fix)
- [Directives](#directives)
- [Pipes](#pipes)
- [Services](#services)
- [Project Structure](#project-structure)

## Installation

### Prerequisites

- **NodeJS**: open-source, cross-platform JavaScript runtime environment and library for running web applications outside the client's browser.

Wait, this **NodeJS** sounds very unneeded. Do I really have to use it for my client-side web application? Well, Angular does not need NodeJS directly but it is required to use it for all the build and development tools. (**npm** comes with NodeJS by default and it allows easy dependency management. It also gives **ng cli** a very useful tool to quickly build an angular project. Finally, it allows you to spin up (= host) a local web server in order to develop your web application)

### Install Angular

```bash
sudo apt install nodejs #Install
node -v          #Check installation
sudo apt install npm    #Install
npm -v           #Check installationls
sudo npm install -g @angular/cli@7.0 #Install Angular 7.0
sudo npm install -g @angular/cli #Install the latest version of Angular
```

### Modify Environment

n is VCS tool for node. It allows to install given versions of Node and more.

Install n
```bash
npm install -g n
```

Install Node
```bash
n 16.13.0   # Install a specific version of Node

n --latest  # Show the latest Node version available
n latest    # Install latest version of Node

n --stable  # Show the latest stable Node version
n stable    # Install latest stable version of Node
```

Remove Node
```bash
n rm <version>  # Remove the given Node version(s)
```

## Create a new Project

First, you have to know that you can't have **more than one** angular project active at the same time. If you already have another angular project, you'll have to delete the *~/.npm* folder. If you don't do so, the **ng new** command will fail. 

### Main commands

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

# OR

ng g c my-component
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

### Known errors

```bash
ng generate component nom-component
```

**Could not find an NgModule. Use the skip-import option to skip importing in NgModule.**

### Quick fix

- If *app.module.ts* is not present, create it in *src/app/*
- Make sure to execute the `ng generate` in the *src/app/* folder

## Directives

Directives are classes that add additional behavior to elements in your Angular applications. They are very useful to dynamically modify elements of the DOM (*Document Object Model*)

The DOM refers to the webpage and all its nodes and objects. Don't forget that a website built with Angular is website with only one webpage.

There are **2 types of directives**:
- Structural directives: to modify elements of the DOM (add/remove)
- Attribute directives: to modify properties of the elements in the DOM

|  **Name** |       **Type**       |                           **Usage**                          |                       **Example**                       |
|:---------:|:--------------------:|:------------------------------------------------------------:|:-------------------------------------------------------:|
|   *ngIf   | Structural Directive | Add elements/components in the DOM if the condition is valid |         _*ngIf = "imageCard.location === Paris"_        |
|   *ngFor  | Structural Directive |             Add all element in a list in the DOM             |             _*ngFor = "let el of elements"_             |
| [ngStyle] |  Attribute Directive |       Dynamically modify a style property of an element      | _[ngStyle] = "{color: 'rgb(0 + imageCard.likes + 0)'}"_ |
| [ngClass] |  Attribute Directive |  Apply a style class to an element if the condition is valid |   _[ngClass] = "{className: buttonText === 'Coucou'}"_  |

## Pipes

Pipes are tools used to format the display of data. Pipes allow us to display an information in differents forms without modifying the original value of the data.

The most used form of pipes is called **String Interpolation**. It is easy to recognize, it uses the syntax `{{blabla | pipeName: instructions }}` where **|** symbolizes the pipe itself. 

Case Pipes
```html
<h2>{{imageCard.title | lowercase }}</h2>   <!-- Display the title in lowercase -->
<h2>{{imageCard.title | uppercase }}</h2>   <!-- Display the title in uppercase -->
<h2>{{imageCard.title | titlecase }}</h2>   <!-- Display the title in titlecase -->
```

Date Pipes
```html
<p>{{ imageCard.creationDate | date: 'short'}}</p>
<p>{{ imageCard.creationDate | date: 'medium'}}</p>
<p>{{ imageCard.creationDate | date: 'longDate'}}</p>
<p>{{ imageCard.creationDate | date: 'longTime'}}</p>
<p>{{ imageCard.creationDate | date: 'd MMMM yyyy at HH.mm'}}</p>
```

Number Pipes
```html
<!-- Decimal Pipe -->

<p>{{ 480087.46 | number: '1.0-0'}}</p>     <!-- 480087 -->

<!-- Percent Pipe -->

<p>{{ 0.336 | percent: '1.0-1'}}</p>     <!-- 0.3% -->

<!-- Currency Pipe -->

<p>{{ 344.36 | currency: 'EUR'}}</p>     <!-- 344.36€ -->
<p>{{ 344.36 | currency: 'EUR': 'code'}}</p>     <!-- 344.36 EUR -->
```

## Services

In Angular, we use files that centralize methods which communicate with the backend server. They are a sort of contact point between frontend and backend. These files are called **Services**. Services are symbolized with `@Injectable`.

In a Service file, there is no `OnInit()` method. Elements are declared and initialized like that:
```typescript
export class ImageCardsService {
    imageCards = [
        {
            ...,
            ...,
            ...,
            ...,
        },
        {
            ...,
            ...,
            ...,
        }
    ]
}
```

Services are located in `src/app/services`.

In order to use a service in a component, we use a **Dependency Injection** (DI):

```typescript
export class ImageCardsComponent {
    constructor(private imageCardsService: ImageCardsService){}
}
```

## Project Structure

```
src/
├────────────────────────── app/
|                            ├── component1/
|                            ├── component2/
|                            ├── componentn/
|                            ├── services/ (interaction point with backend)
|                            ├── app.component.html
|                            ├── app.component.scss
|                            ├── app.component.ts
|                            ├── app.component.spec.ts
|                            └── app.module.ts
├──────────── assets/
├── environment/
├── angular.json
└── index.html
```