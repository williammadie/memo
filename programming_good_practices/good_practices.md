# Programming Good Practices

## Table of content

- [Simplify Your Code](#simplify-your-code)
	- [Build according to Cognitive Complexity](#build-according-to-cognitive-complexity)
	- [Avoid Nested Ifs with If Guards](#avoiid-nested-ifs-with-if-guards)
		

## Simplify Your Code

### Build according to Cognitive Complexity

**Cognitive Complexity** is referred as **measure of how difficult a unit of code is to intuitively understand**. So **Cognitive Complexity** is the indicator of **understandability**.

Such measurement can be done in details by **linters** (= a tool that analyzes source code and looks for security issues, typos, code smells and suggests changes).

How is it measured?

It is mainly related to the **logic flow**. If it is from top to bottom, it is very easy to understand. In the case of deviation of the logic flow, the function's cognitive complexity increases.

What are the elements which break the logic flow?

- conditionals (= they divide the flow into separated units of code before resuming to a single one)
- loops (= they break the top-to-bottom flow by looping in circle)
- try-catch blocks
- switch cases
- sequences of logical operators (= boolean arithmetic can quickly become very complicated to understand (e.g. a || b && c || d)
- recursion (= one the most complicated thing to understand for the reader as the flow can return at the beginning of the function but with new values)
- jumps to label (= it reverses the basic logic flow by doing a bottom-to-top action)
- nested conditionals / nested loops (= the more it is nested, the harder it is to read and understand for an external reader)

### Avoid Nested Ifs with If Guards

According to what we've learned about the cognitive complexity, it is now time to learn how to reduce it by simple changes in our code:

The below function is very difficult to read because it relies on what is called a **nested if**. Even with such simple instructions, it can quickly increase its **cognitive complexity**.
```python
def function(user: User, server: Server):
	if server.isOnline:
		if areValid(user.credentials):
			if user.isconnected():
				server.processOperation(user)
			else:
				loggger.log("Cannot proceed: User is not connected")
		else:
			logger.log("Cannot proceed: User credentials are not valid")
	else:
		logger.log("Cannot proceed: Server is offline")
```

Start using **If Guards** by using the **negation** of each and every condition. There is no more indented parts, no more else block and the final operation is at the very end of the function.
```python
def function(user: User, server: Server):
	if not server.isOnline:
		logger.log("Cannot proceed: Server is offline")		
		return
	
	if not areValid(user.credentials):
		logger.log("Cannot proceed: User credentials are not valid")
		return
		
	if not user.isconnected():
		loggger.log("Cannot proceed: User is not connected"):
		return
		
	server.processOperation(user)
```

When am I able to use **If Guards**?
Mainly when you realize that all actions in your function are engulfed in a condition. (In the above example, all actions are done only if the user *is online*.
