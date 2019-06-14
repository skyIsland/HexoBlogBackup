title: 'C# 引用类型传参'
author: ismatch
tags:
  - 'C#'
categories: []
date: 2018-12-21 00:00:00
---
*  一直不知道引用类型作为参数传入方法内会有怎样的改变，还停留在引用类型是引用堆的地址的层次上（停留在概念）...
* 今天遇到一个问题，遂亲自测试以及问大佬，终于弄清楚一个道理，在此记录一下...
> 引用类型作为参数传入方法内，传递的为堆的地址，所以如果在方法内对引用类型的数据做出改变，会影响所有引用了该堆地址的数据。
- 实际测试
![](http://img.ismatch.cn/refparameter.png)
- C#本质论的解释
![](http://img.ismatch.cn/refvaluecompare.jpg)