# PHP

## Table of Contents

- [What is the WEB](#what-is-the-web)
- [In the WEB classic](#in-the-web-classic)
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

## In the WEB classic

Each request triggers a reloading of the webpage.

In modern websites, requests uses AJAX (Asynchronous JavaScript And XML) systems so this reloading is not needed. 

## Introduction

PHP has been invented in 1994 by Rasmus Lerdof for building his website. In 1997, 2 students reworked the **PHP core** that became PHP 3 and then PHP 4. They created the `Zend` society. It is now in PHP 8.

PHP is often used with an Apache or NGINX server but it has its own runtime environment and can be used alone.

## Structure

PHP files can contain both `HTML` and `PHP` languages. It is defined with tags `<?php my-code ?>`.
If the file **contains only PHP**, we don't need to use `<?php ... ?>`.

PHP instructions always end with `;`.

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

## Select

$pdo->query($query)->fetchAll();

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