# Design Patterns

## Table of Contents

- [Creational Design Patterns](#creational-design-patterns)
    - [Singleton Pattern](#singleton-pattern)

## Creational Design Patterns

### Singleton Pattern

It is one of the simplest **design pattern**. Its goal is to ensure that a class has **only one instance** while providing a global access point to this instance.

```php
$pdo = null;

function getPDO() {
    if ($pdo == null) {
        ...
    }
    return $pdo;
}
```