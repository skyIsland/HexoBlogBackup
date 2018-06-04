title: .Net基础-垃圾回收
author: ismatch
tags:
  - .Net基础
  - ''
categories: []
date: 2018-03-20 22:30:00
---
##### 常规的垃圾回收策略：

- 类中没有非托管资源，且没有对象实现IDisposible: 什么也不用做。
- 类中没有非托管资源，且有对象实现IDisposible: 特别注意这些对象，确保调用了它们的Dispose方法（显式或者隐式的）。你可以实现IDisposible，然后实现Dispose方法，在其中释放资源。
- 类中有非托管资源: 跟从微软模板，实现一个私有函数释放托管和非托管资源，实现IDisposible，然后实现Dispose方法，并在其中调用私有函数，然后呼叫GC.SuppressFinalize（第一道闸）。实现一个解构函数，并在其中调用私有函数（第二道闸）。如果你的第一道闸完美无缺，第二道闸是没有机会上场的。

- 参考链接

[垃圾回收：概念与策略](http://www.cnblogs.com/haoyifei/p/5680745.html)