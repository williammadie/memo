# Clean Code

## Table of Contents

- [Introduction](#introduction)
- [Error Handling](#error-handling)
- [Other tips](#other-tips)

## Introduction

All advices in this file are based on **Clean Code** by *Robert C. Martin*.

## Error handling

### Use exceptions rather than return codes

Historically, programming languages like C used `return codes/error codes` that were returned from incriminated methods. This is a pretty annoying habit as it forces the caller **to check the error status**.

Moreover, checking the error status is easily forgettable and error-prone.

### Write your `try-catch-finally` statement first

By doing so, you will construct your code like a SQL transaction. The `try` block allows the possibility to escape if any unexpected behaviors happen. So, the `catch` block should let our code in a consistent state.

### Use unchecked exception

Checked exceptions are not such a great idea. Why?

- if you throw an exception and the `catch` is three levels above, you must declare that exception in the signature of each method between you and the `catch`. This violates the **Open Closed Principle** as a change at low-level forces higher-level changes.

### Provide context with Exceptions

### Don't return `null`

When we create a method that returns `null`, we are **essentially** creating work for ourselves. Why?

=> Because this will force us to check whether our return value is null later in our code. If we have a lot of methods that return `null`, we'll have a lot of null checks and our code will become less readable.

So what do we do if we can't return `null`?

There are two solutions:
1. You can throw an exception.
2. You can return a *special case object*. (these are essentially objects like `Collections.emptyList();`)

### Don't pass `null`

By default, we should forbid passing `null` to a method. But what does it mean concretly? Do we have to add a `null` check at the beginning of our method?

The answer is **no**. If you never return `null`, you'll never have to check for `null` values in your methods.

## Other tips

### Using assertions for developing and testing

**Important Note**:
- By default, assertions are disabled in the *JVM*. So it makes them
quite dangerous as they can be skipped if the environment is not well configured.
- Assertions should not be used as a replacement for proper input validation or error handling in production code. 

The following method could be used with `if` and `.equals()`, 
however it is far more readable for a human written with assertions
```java
public void registerNew(DomainObject obj) {
    Assert.notNull("id not null", obj.getId());
    Assert.isTrue("object not dirty", !dirtyObjects.contains(obj));
    Assert.isTrue("object not removed", !removedObjects.contains(obj));
    Assert.isTrue("object not already registered new", !newObjects.contains(obj));
    newObjects.add(obj);
}
```

A valid approach for both development, test and production would be to use a dependency like `rlang3` from Apache Commons or `guava` from Google.