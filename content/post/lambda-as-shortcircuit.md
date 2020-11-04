---
title: "Lambda as short circuit"
date: "2020-11-04"
author: "Viktor"
---

### Lambda 

The principal aim of lambda in java is to make more readable and concise code. For that java lambda has the following property : 
- They are anonymous function because you don't need to name them
- In opposition to method they are not attached to a particular class.
- You can pass them around as argument to other methods and stored them.

#### Normal order

**Normal order** is about executing a function only if it's needed. In opposition to **applicative order** where what we see when we read the code is executed.
When some function is not executed due to normal order that can improve performance. One of the commons ways to do that in old java version is Short-circuit evaluation.

```java
public void shortCircuit(){
 	int trigger = 8;
    
    if(trigger > 10 && veryExpensiveFunction()){
        //do thing
    }
}
```

Here due to short-circuit ```veryExpensiveFunction()``` is not called, because the first condition ```trigger > 10``` is false.

#### Eager vs Lazy evaluations
Eager evaluation is when the code follow the execution flow. We see a function call and then it's been evaluated at the same time. 

```java
public void shortCircuit(){
 	int trigger = 8;
    
    boolean expensiveResult = veryExpensiveFunction();
    if(trigger > 10 && expensiveResult){
        //do things
    }
}
```

If we write the previous function this way, we can see that we lose the advantage of short-circuit and due to the eager evaluation the ```veryExpensiveFunction()``` is executed without we need its result.

```java
public void shortCircuit(){
 	int trigger = 8;
    
    final Supplier<Boolean> expensiveResult = () -> veryExpensiveFunction();
    if(trigger > 10 && expensiveResult.get()){
        //do things
    }
}
```
Here a way to write this in java 8+, the veryExpensiveFunction is not executed before we really need it's result.