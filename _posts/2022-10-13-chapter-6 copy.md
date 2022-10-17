---
layout: detail
type : 2
keyword : C++ Network Programming Volume
title: C++ Network Programming Volume ：Chapter 6
description: An Overview of Operating System Concurrency Mechanisms
---

## CHAPTER 6
## An Overview of Operating System Concurrency Mechanisms

### 同步事件多路分离

select/Poll用于在一组事件源上等待特定事件的发生。当某个（或多个）事件源被激活时，函数将返回至调用者。于是，调用者就可以处理这些”来自多个源“的时间。同步事件多路分离是反应式服务器的基础。


### 互斥锁

阻塞,串行地访问共享数据
递归互斥锁：拥有互斥锁的线程可以多次获得它而不会产生死锁，只要这个线程最终以相同的次数释放这个互斥锁即可   
非递归互斥锁：如果当前拥有互斥锁的进程在没有首先释放它的情况下，试图再次获得它，就会导致死锁而失败。

### 读写锁

读共享，并行处理  
写独占，写的优先级高

### 信号量锁

阻塞的线程只有在另一个线程发布信号量后才会被释放  
此功能允许在更广泛的执行上下文中使用信号量，例如信号处理程序或中断处理程序

### 条件变量

条件变量提供了与互斥锁、读取器/写入器或信号量锁不同的同步方式。后三种机制使其他线程等待，而持有锁的线程在临界区执行代码。相反，线程可以使用条件变量来协调和安排自己的处理。