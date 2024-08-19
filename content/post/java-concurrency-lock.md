---
title: "Java Synchronized vs ReentrantLock locking"
date: "2024-08-04"
author: "Marlon"
---

In this article we will explore the basic building block to do synchronization know as `intrinsic locking` and the high level synchronization
offer by the `java.util.concurrent` package. 

Please anwser the following question : 
- What is the purpose of lock ?
- Each instance class object have 'monitor lock, entry set and wait set' assigned to them. Describe the impact of each one, and describe when each one is modified
- What does it means to be reentrant ? 
- Describe the different way to coordinate communication between two threads and their impact on the thread lifecycle using low level synchronization constructs.
  - synchronize : Where can we use it and what can be synchronize ?
  - Wait/Notify
  - Notify vs NotifyAll : When would you use notify and notifyAll
  - Interrupt : What happened if we interrupt a running thread or a thread not yet start ?
  - What is the impact of calling join on the daemon thread? 
  - Does yield guarantee other threads will be executed? 

## Instrinsic locks

First what is intrinsic locks, it's the most basic building block the Java language provide to synchronize thread.

### What is the purpose of lock ?

- If you need only one thread to access an resource (mutex), synchronize is what you need.
- If you need an condition to be true for an exclusive access to an resource (monitor)


Ressources : 
- https://docs.oracle.com/javase/tutorial/essential/concurrency/locksync.html
- https://www.infoworld.com/article/2168239/how-the-java-virtual-machine-performs-thread-synchronization.html
