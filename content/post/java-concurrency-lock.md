---
title: "Java Synchronized vs ReentrantLock locking"
date: "2024-08-04"
author: "Marlon"
---

In this article we will explore the basic building block to do synchronization know as `intrinsic locking` and the high level synchronization
offer by the `java.util.concurrent` package. 

Please anwser the following question : 
- What is the purpose of lock ?
- What does it means to be reentrant ? 
- Describe the different way to coordinate communication between two threads and their impact on the thread lifecycle using low level synchronization constructs.
  - synchronize : Where can we use it and what can be synchronize ?
  - Wait/Notify
  - Notify vs NotifyAll : When would you use notify and notifyAll
  - Interrupt : What happened if we interrupt a running thread or a thread not yet start ?
  - What the impact of calling join on the deamons thread ? 
  - Does yield guarante other thread will be executed ? 
## Instrinsic locks

