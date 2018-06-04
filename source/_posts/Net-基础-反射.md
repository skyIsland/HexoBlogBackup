title: .Net 基础-反射
author: ismatch
tags:
  - .Net基础
categories: []
date: 2018-03-20 22:45:00
---
- 定义

> 在.NET中，查看和操作元数据的动作称为反射（也称为元编程）。

![image](/files/Reflection.jpg)

- 使用

<!--more-->
> 你需要先使用Assembly.Load或LoadFrom方法找到程序集，然后你可以使用GetType获得该程序集的一个类型，最后，使用Activator.CreateInstance（你获得的类型对象）创建该类型的一个实例。

1.准备好的程序集
```
namespace ReflectionDLL
{
    public class Class1
    {
        public int aPublicField;
        private int aPrivateField;
        public int aPublicProperty { get; set; }
        private int aPrivateProperty { get; set; }

        public event EventHandler aEvent;

        //Ctor
        public Class1()
        {

        }

        public void HelloWorld()
        {
            Console.WriteLine("Hello world!");
        }

        public int Add(int a, int b)
        {
            return a + b;
        }
    }
}
```
2.在控制台程序调用

```
namespace ReflectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Assembly a = null;

            try
            {
                a = Assembly.LoadFile(@"D:\Code\Sky.2018Test\DLL\ReflectionDLL.dll");
            }
            catch (Exception ex)
            {
                //Ignore
                Console.WriteLine($"加载程序集发生错误,原因{ex.Message}");
            }

            if (a != null)
            {
                CreateUsingLateBinding(a);
            }
            Console.ReadKey();
        }

        static void CreateUsingLateBinding(Assembly asm)
        {
            try
            {
                /*
                 * 不用var 方便一眼看出当前返回的是什么类型 不用鼠标点上去看是什么类型
                 */
                // 获得类型实例
                Type t = asm.GetType("ReflectionDLL.Class1");

                // 晚期绑定建立一个Class1的实例
                object obj = Activator.CreateInstance(t);

                // 获得一个方法
                MethodInfo mi = t.GetMethod("HelloWorld");

                // 方法的反射调用执行(没有参数) 感觉像是js.call() 是什么类型调用什么方法
                mi.Invoke(obj, null);
            }
            catch (Exception ex)
            {

                Console.WriteLine($"发生错误,原因{ex.Message}");
            }
        }
    }
}
```

注意，这样创建的类型实例是Object类型。（C# 4引入了动态类型之后，也可以用dynamic修饰这种类型的实例）这个类型对象的方法都不可见，如果要使用它的方法，只能使用反射（例如使用GetMethods获得方法信息，然后再Invoke）。这是反射最普遍的应用场景。
- 参考链接

[反射](http://www.cnblogs.com/haoyifei/p/5730284.html)