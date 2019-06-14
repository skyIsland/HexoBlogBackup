title: .Net框架理解笔记
author: ismatch
tags:
  - .Net基础
categories: []
date: 2019-05-07 22:50:00
---
####  1.CIL——公共中间语言（Common Intermediate Language）
> 经过编译器编译之后，所生成的程序集就是由CIL语言代码描述的。（IL）
- 公共。基于.Net平台运行
- 中间。介于机器码与C#(或者其他基于.Net平台运行的语言)之间的语言，同时还需要.Net运行时环境的支持
- 语言。基于堆栈的语言，面向对象。


<!-- more -->

> 由于程序集是由CIL语言所描述的，因此CIL也叫做程序集语言（Assembly Language）。又因为.NET程序集需要由.NET运行时加载才能运行，可以视其为由.NET运行时进行管理的，所以CIL代码也叫做托管代码（Managed Code）。相对的，不需要.NET运行时就可以执行的代码就叫做非托管代码（Unmanaged Code）。

#### 2.1 BCL——基类库（Base Class Library）
- mscorlib.dll程序集

![image](http://img.tracefact.net/tech/netframework/07.png)
- CIL类型，基元类型

CIL 类型 | C# 关键字 | VB.NET关键字
---|---|---
System.Byte | byte | Byte
Sytem.Int16 | short | Short
System.Int64 | long | Long

#### 2.2 FCL——框架类库（Framework Class Library）
- BCL从属于FCL
- 最内一层，由BCL的大部分组成，主要作用是对.NET框架、.NET运行时及CIL语言本身进行支持，例如基元类型、集合类型、线程处理、应用程序域、运行时、安全性、互操作等。 
- 中间一层，包含了对操作系统功能的封装，例如文件系统、网络连接、图形图像、XML操作等。 
- 最外一层，包含各种类型的应用程序，例如Windows Forms、Asp.NET、WPF、WCF、WF等。

#### 3. CTS——公共类型系统（Common Type System）
- 一套定义了语言可以做什么，不可以做什么，具有哪些特性的规则
    - 任何满足了这套规则的高级语言就可以称为面向.NET框架的语言
    - 比如定义类、结构、委托等类型，访问性，约束（单继承基类，隐式继承Object...）

#### 4. CLS——公共语言规范 （Common Language Specification）
- 语言特性要一致
    - 是否区分大小写，标识符的命名规则如何，可以使用的基本类型有哪些，构造函数的调用方式（是否会调用基类构造函数），支持的访问修饰符等
- CLS是CTS的一个子集

#### 5. CLR——公共语言运行时（Common Language Runtime）/.NET运行时（.NET runtime）
> CLR是一个软件层或代理，它管理了.NET程序集的执行，主要包括：管理应用程序域、加载和运行程序集、安全检查、将CIL代码即时编译为机器代码、异常处理、对象析构和垃圾回收等。CLR是使用非托管代码编写。
- 了解程序集
    - 程序集包含了CIL语言代码，而CIL语言代码是无法直接运行的，需要经过.NET运行时进行即时编译才能转换为计算机可以直接执行的机器指令。
    -  所有在Windows操作系统上运行的程序都需要符合PE/COFF文件的格式
![image](http://img.tracefact.net/tech/netframework/18.png)    

- 运行程序集（当操作系统尝试打开一个托管程序集（.exe）时）
    - 首先会检查PE头，根据PE头来创建合适的进程
    - 进一步检查是否存在CLR头，如果存在，就会立即载入MsCorEE.dll（.NET框架的核心组件之一）
    - 加载了MsCorEE.dll之后，会调用其中的_CorExeMain()函数，该函数会加载合适版本的CLR
    - 在CLR运行之后，程序的执行权就交给了CLR。CLR会找到程序的入口点，通常是Main()方法，然后执行它。
        - 加载类型。在执行Main()方法之前，首先要找到拥有Main()方法的类型并且加载这个类型。CLR中一个名为Class loader（类加载程序）的组件负责这项工作。它会从GAC、配置文件、程序集元数据中寻找这个类型，然后将它的类型信息加载到内存中的数据结构中。在Class loader找到并加载完这个类型之后，它的类型信息会被缓存起来，这样就无需再次进行相同的过程。在加载这个类以后，还会为它的每个方法插入一个存根（stub）。
   
        - 验证。在CLR中，还存在一个验证程序（verifier），该验证程序的工作是在运行时确保代码是类型安全的。它主要校验两个方面，一个是元数据是正确的，一个是CIL代码必须是类型安全的，类型的签名必须正确。

        - 即时编译。这一步就是将托管的CIL代码编译为可以执行的机器代码的过程，由CLR的即时编译器（JIT Complier）完成。即时编译只有在方法的第一次调用时发生。回想一下，类型加载程序会为每个方法插入一个存根。在调用方法时，CLR会检查方法的存根，如果存根为空，则执行JIT编译过程，并将该方法被编译后的本地机器代码地址写入到方法存根中。当第二次对同一方法进行调用时，会再次检查这个存根，如果发现其保存了本地机器代码的地址，则直接跳转到本地机器代码进行执行，无需再次进行JIT编译。

 
![image](http://img.tracefact.net/tech/netframework/19.png)

#### 6.  CLI——公共语言基础(Common Language Infrastructure)
> 实际上本章的每一小节都是这个标准的一部分。CLI包括：CIL、CTS、CLS、VES、元数据、基础框架。

#### [学习链接](http://www.tracefact.net/tech/042.html)