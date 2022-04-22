# World Wide Web

## Table of Contents

- [Browse the Web](#browse-the-web)
    - [HTTP Methods](#http-methods)
    - [HTTP Status Codes](#http-status-codes)
- [RESTful & RESTless APIs](#restful-&-restless-apis)
    - [APIs](#apis)
    - [RESTful APIs](#restful-apis)
    - [RESTless APIs](#restless-apis)

## Browse the Web

### HTTP Methods

| HTTP Methods |      CRUD      |                  Description                 |
|:------------:|:--------------:|:--------------------------------------------:|
|     POST     |     Create     | Used to transfer a local resource to the API |
|      GET     |      Read      |       Used to obtain a distant resource      |
|      PUT     | Update/Replace |     Used to overwrite a distant resource     |
|     PATCH    |  Update/Modify |       Used to modify a distant resource      |
|    DELETE    |     Delete     |            Delete distant resource           |

### HTTP Status Codes

**HTTP Methods** return what's called **Status Codes**. It allows the user to know if his request was successful, failed or is still being processed.

Each code belongs to *a specific category* and *has a meaning* which can be found here: https://developer.mozilla.org/fr/docs/Web/HTTP/Status

These **Status Codes** are very useful when it comes to automate a process that needs to communicate with an API. Depending on the returned code, the developer has the ability to orient and create a proper response in his program.

![http-status-codes](/web/web/resources/http-status-codes.png)

## RESTful & RESTless APIs

### APIs

The Web is full of **APIs** which stands for **Application Programming Interface**. Basically, an **API** is a service that developers use to access data generated or stored in an application **they do not own (most of the time)**. It allows someone to access data without having to know how this data is handled by the application. The only thing the client has to know is how to retrieve the information.

![img_1](/web/web/resources/api-mechanism.jpg)

There are different types of APIs. There are *public and private* APIs. Public ones can be accessed without any key. It is generally ruled by limits which can be, for instance, a maximum number of requests per minute. Private APIs' access is restricted to people having authorized credentials. It can be part of a paid service.

### RESTful APIs

A **RESTful** service is a service based on the REST (*REpresentational State Transfer*) architectural style. It can be seen as a box containing a bunch of uniquely adressable entities whose goal is to be accessed via a *web application (API)*. The REST architecture defines how these entities can be accessed/modified/downloaded/deleted through **HTTP Methods**.

### RESTless APIs

A **RESTless** service is a service that does not conform to the REST architecture.