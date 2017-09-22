## 1.二叉树的递归和非递归实现

## 2.求二叉树两个节点最短路径



## 3.String为什么设计成不可变

-常量池的保证，如果引用的对象可变换将失去常量池的意义

-安全性考虑，传入方法的参数不可变

-HashSet、HashMap作为key，如果可变会出现不可预知的错误

4.内存泄漏如何分析，分析工具\(Android\)

5.链表逆序

6.序列化的作用

7.List和Map的实现方式和存储方式

8.静态内部类的设计意图

-首先理解静态内部类\(Nested Static Class\)和内部类的区别\(inner class\)

在非静态内部类中不可以声明静态成员，只有静态内部类才能够定义静态的成员变量与成员方法。

非静态内部类，可以随意的访问外部类中的成员变量与成员方法。即使这些成员方法被修饰为private\(私有的成员变量或者方法\)。不能够从静态内部类的对象中访问外部类的非静态成员\(包括成员变量与成员方法\)

在创建内部类之前要先在外部类中要利用new关键字来创建这个内部类的对象，而静态内部类中不需要

再来看看builder模式,为什么builder模式的builder要设计成静态内部类

I think that the reason for doing this is so that the inner class \(the Builder\) can access private members of the class that it is building

[https://softwareengineering.stackexchange.com/questions/225207/why-should-a-builder-be-an-inner-class-instead-of-in-its-own-class-file/225210\#225210](https://softwareengineering.stackexchange.com/questions/225207/why-should-a-builder-be-an-inner-class-instead-of-in-its-own-class-file/225210#225210)

9.线程如何关闭,如何防止线程的内存泄漏

