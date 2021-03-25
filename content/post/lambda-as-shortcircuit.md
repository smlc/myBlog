---
title: "Lambda as short circuit"
date: "2020-11-04"
author: "Viktor"
---

## Lambda 

The lambda's principal aim in java is to make more readable and concise code. For that, Java lambda has the following property: 

- They are anonymous function because you don't need to name them 
- In opposition to a method, they are not attached to a particular class. 
- You can pass them around as an argument to other methods and stored them.

### Normal order

**Normal order** is about executing a function only if needed in opposition to **applicative order** where what we see when we read the code is executed.
When some function is not executed due to normal order, performance can improve. One of the commons ways to do that in the old java version is Short-circuit evaluation.

```java
public void shortCircuit(){
 	int trigger = 8;
    
    if(trigger > 10 && veryExpensiveFunction()){
        //do thing
    }
}
```

Here due to short-circuit ```veryExpensiveFunction()``` is not called, because the first condition ```trigger > 10``` is false.

### Eager vs Lazy evaluations
Eager evaluation is when the code follows the execution flow. We see a function call, and then it's been evaluated simultaneously. 

```java
public void shortCircuit(){
 	int trigger = 8;
    
    boolean expensiveResult = veryExpensiveFunction();
    if(trigger > 10 && expensiveResult){
        //do things
    }
}
```

Let's write the previous function this way. We can see that we lose the advantage of short-circuit. Due to the eager evaluation, the ```veryExpensiveFunction()``` is executed without we need its result.

```java
public void shortCircuit(){
 	int trigger = 8;
    
    final Supplier<Boolean> expensiveResult = () -> veryExpensiveFunction();
    if(trigger > 10 && expensiveResult.get()){
        //do things
    }
}
```
This is the way to write a short-circuit in java 8+ using lambda. The ```veryExpensiveFunction()``` is not executed before we need his result.

