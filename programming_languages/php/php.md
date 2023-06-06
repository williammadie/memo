# PHP

## Table of Contents

- [What is the WEB](#what-is-the-web)
- [In the WEB classic](#in-the-web-classic)
- [What is a framework](#what-is-a-framework)
- [Introduction](#introduction)
- [Structure](#structure)
- [Variables](#variables)
- [Strings](#strings)
- [Include and Require](#include-and-require)
- [Forms](#forms)
- [Classes](#classes)
- [Exceptions](#exceptions)
- [Sessions](#sessions)
- [Development Server](#development-server)
- [Select](#select)
- [Serialize and Unserialize](#serialize-and-unserialize)

## What is the WEB

It was invented in 1989 by the CERN (Centre de Recherche Européen) in order to exchange information.

It is based on the `client-server` model. The client is said to be "light" because the user doesn't have to download anything in order to access the service. The WEB is based on HTTP requests which are divided into two parts:

- header: request metadata
- body: content of the request

1. Client sends an HTTP request to the server
2. Server receives request and handles it by performing requested action
3. Server responds to the initial request

![client-server-architecture](/programming_languages/php/resources/client-server-architecture.png)

## In the WEB classic

Each request triggers a reloading of the webpage.

In modern websites, requests uses AJAX (Asynchronous JavaScript And XML) systems so this reloading is not needed. 

- `Frontend`: Code executed on the client-side (on a web browser)
- `Backend`: Code executed on the server-side.

## MVP

PHP uses **MVP** (**Model View Presenter**).
- `model`: business logic
- `presenter`: application logic
- `view`: ui components

It is recommended to have **1 controller** for each page.


## What is a Framework

**framework**: set of ready-made components or solutions made in order to speed up development.

A framework is not a library. It is **more generic** and can be used in different context. It can has several functions. It also often enforces an architecture.

Frameworks are used to **structure an application**, to **facilitate debug and maintainability**. It also **enhances **security, performance and quality**.

It handles **technical logic** and let **business logic** for the developer.

PHP Framework:
- `Symfony`
- `Zend Framework`
- `LARAVEL`

There are also **serverless frameworks**.

## Introduction

PHP has been invented in 1994 by Rasmus Lerdof for building his website. In 1997, 2 students reworked the **PHP core** that became PHP 3 and then PHP 4. They created the `Zend` society. It is now in PHP 8.

PHP is often used with an Apache or NGINX server but it has its own runtime environment and can be used alone.

PHP is a `backend` language. (It is `server-side`).

## Structure

PHP files can contain both `HTML` and `PHP` languages. It is defined with tags `<?php my-code ?>`.
If the file **contains only PHP**, we don't need to use `<?php ... ?>`.

PHP instructions always end with `;`.

### Project Structure

- `db.php`: in this file we can put a PDO getter to obtain the object used to access databases.

Repository, DAO, Services => It all refers to the code that is responsible for accessing databases.

In Web development, there are generally *2 preferred architectures*:
- Architecture by layers:
    - controllers/
    - services/
- Architecture by module/concept:
    - pokemon/
        - controller.php
        - Pokemon.php (Model)
        - pokemon-service.php

Depending on the **framework** we use, we can use one or another. Keep in mind that most frameworks recommend a specific architecture.

## Variables

PHP is a **a dynamically and weakly typed programming language**.

In PHP, all variables are prefixed by `$`. For instance:
```php
$myVariable = 56;
```

## Strings

PHP can handle indistinctively `"` and `'`.

It is possible to print text with `echo "Hello World"`.

## Include and Require

They are used to manage libraries. Require triggers an error if the file is not found.

## Forms

Data which is exchanged through forms can be retrieved with:
- `$_GET`
- `$_POST`
- `$_REQUEST`

Client-side form
```html
<form method='get'>
    <input name='foo'>
    ...
</form>
```


```php
$_GET['foo'] : access to the variable stored in the request array
```

## Classes

Define a class
```php
<?php

class Foo {
    public static $var;
    public static function myStaticFunction() {
        ...
    }

    public function myInstanceFunction($param) {
        ...
    } 
}
?>
```

Use static functions and access static variables
```php
<?php
require 'foo.php';

Foo::myStaticFunction();
Foo::$var

$myObject = new Foo();
$myObject -> myInstanceFunction(12)
?>
```

## Exceptions

```php
throw new Exception("...");
```

```php
catch
```

```php
custom exception
```

## Sessions

Sessions are used to create a context/memorize information. There are two types of sessions:

- Server session: Handled by the PHP server
- Client session: Handled by the web browser

Sessions can be used by users to log in and access content which is not accessible when not logged in. Users can then navigate to other pages and stay **logged in**.

Create a session
```php
session_start()
// This creates an array called SESSION
// We can put what we want into this array
```

Close a session
```php
session_destroy()
```

Store an object into the session array
```php
$_SESSION['myObject'] = serialize($myObject);
```

Retrieve an object from the session array
```php
$myObject = unserialize($_SESSION['myObject']);
```

## Development Server

With PHP > 5.4, you can run a development server:

```bash
php -S 127.0.0.1:8000
```

## SQL

PHP uses a *PDO* (*PHP Data Object* to access databases). 

Requests can be **executed directly** or **prepared**:
- executed directly: great for requests with no outside parameters
- prepared: optimized requests thanks to PDO library cache system.

At each request, PHP forgets all context. It has to re-open a connection to the database for example.

### Select

```php
$pdo->query($query)->fetchAll();
```

### Insert


```php
function addPokemonToDb($pokemon,$pdo) {
    $query = 'INSERT INTO pokegame.pokegame (CODEPOKE, NOM, EVOL, TYPEPOK) VALUES (:id, :name, :evol, :type);';
    $prep = $pdo->prepare($query);
    $prep->bindValue(':id', $pokemon->getId(), PDO::PARAM_INT);
    $prep->bindValue(':name', $pokemon->getNom(), PDO::PARAM_STR);
    $prep->bindValue(':evol', $pokemon->isEvolution(), PDO::PARAM_BOOL);
    $prep->bindValue(':type', serialize($pokemon->getType()), PDO::PARAM_STR);

    $prep->execute();
}
```

## Serialize and Unserialize

print objects in their raw form
```php
print_r($myObject);
```

In order to store an object, you'll sometimes need to **serialize** it. It means to make it flat/turn it into a string representation. In PHP, it is actually possible to store any object in a string representation, through the `serialize()` function.

A serialized object can then be retrieved in its object form through `unserialize()`

serialize an object
```php
serialize($myObject);
```

unserialize an object
```php
unserialize($objectStringRepresentation)
```

How does this work?

The string produced by the `serialize()` function has the following form:
```php
"a:1:{i:0;s:3:"Fire";}"
```

Let's get our object back!

- `a` means that the object is an `array`
- `1` means that the array has a length of `1`
- `i:0` means that the following value is the first one (index of 0)
- `s:3` means that the following value is a `string` of length `3`
- `Fire` is the actual value described by `i:0` and `s:3`

With all the above information, we know exactly what is the object and can create it back with `unserialize()`