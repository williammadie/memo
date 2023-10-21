# Design Patterns

## Notes for presentation

- don't mention a pattern if it wasn't introduced to the class
- use the quizz for reminding previous information to public
- use examples **written in Java** (best option: implement it yourself)

## Lazy Load

Summarized: You only create or load an object when it's requested, not beforehand. 

This is useful for objects that are **resource-intensive** or not always **needed immediately**. It saves time and resources by avoiding unnecessary work upfront.

### Lazy Initialization

- **Lazy initialization**: The expensive object is retrieved the first time we need it.

```java
public ExpensiveObject getExpensiveObject(String id) {
    if (expensiveObject == null) {
        expensiveObject = expensiveService.findbyName(id) 
        // Initialize the object if not done already
    }
    return expensiveObject;
}
```

**Note**: Frameworks sometimes propose this implementation without us having to create it from scratch.

- **Virtual Proxy**
- **Value Holder** 
- **Ghost**

## Gateway

gateway: ([FR: passerelle]) component used as an intermediate between 

When we communicate with an external system, we have to use a gateway. It hides technical complexity to business logic classes.

## Unit of Work

summarized:  

What is the difference between Repository pattern and Unit of Work?

