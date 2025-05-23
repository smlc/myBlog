---
title: "Go and Java concurrency model"
date: "2025-02-13"
author: "Marlon"
---

## Computation: Virtual thread and Goroutines

Both Java virtual threads and Go goroutines are what we call user-space threads. So what is a user-space thread, opposite to Kernel threads (e.g. Thread class in Java) User-space threads are often managed by the language runtime. This means the language will manage and schedule workload, and context switch between OS threads for you.

They are also more lightweight than Kernel threads because they have a smaller memory footprint, don’t need to involve OS calls, and have faster context-switching than Kernel threads.

## Communication Models: Channel vs Share Memory Communication

### Share memory communication

In Java, the historical way for threads to share data was to use lock primitives to synchronize access to data between different threads.

{{< image src="/img/JavaVirtualThreadSharedMem.png" alt="Java threads shared data through shared memory" position="center" style="border-radius: 8px;" >}}


For example, one thread may write some data into our shared memory space and then want another thread to consume or modify that data. However, this situation can lead to various errors and scenarios that we, as developers, need to manage, such as:

- Spurious Wakeup
- Race Conditions
- Data Visibility
- Deadlock
- Starvation

And many others…

### Channel communication

In Java, we saw that threads shared access to the same data and needed synchronization. 
But in fact, under the hood, the Go channel also has a shared data structure, but why the Go developer doesn't have to deal with synchronization? Once you put data into the channel, Go will make a copy, which means the goroutines don't have to access the same data in memory. 

What made concurrency issues difficult is that you have to deal with two or three of those parameters:

- Shared: data used by more than one thread
- Mutable: data being updated
- State: data storage

What Go channels is doing is deleting the shared aspect of the concurrency problem. 

{{< image src="/img/GoroutineChannel.png" alt="Go routing shared data through channel" position="center" style="border-radius: 8px;" >}}


## Conclusion

The goal of this blog post it’s not to say what is best, but when learning another language, I like to try to see which approach 
the language designer took to solve common problems we found in any language, here concurrency. 
It helps me understand how I can implement solutions in that new language and use my existing knowledge as an anchor so 
I can focus on the new syntax rather than the concept. 

Ressources : 

- **Rethinking Classical Concurrency Patterns - Bryan C. Mills**:  https://www.youtube.com/watch?v=5zXAHh5tJqQ&ab_channel=GopherAcademy
- **The Scheduler Saga - Kavya Joshi:** https://youtu.be/YHRO5WQGh0k?si=9UswJsG5m3zM9Ow_
- **Codewalk: Share Memory By Communicating:** https://go.dev/doc/codewalk/sharemem/
- Java **Creating a Virtual Thread:** https://docs.oracle.com/en/java/javase/21/core/virtual-threads.html#GUID-A0E4C745-6BC3-4DAE-87ED-E4A094D20A38
- **JEP 425: Virtual Threads:** https://openjdk.org/jeps/425
- **Java virtual threads vs Golang Goroutines:** https://www.linkedin.com/pulse/java-virtual-threads-vs-golang-goroutines-zetahive-qbzzc/
