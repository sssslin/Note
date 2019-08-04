# lambda表达式与stream API

从LearningJDK这个项目的提交记录下，可以看到这位大佬在阅读源码的时候非常的有条理，

比如说，大佬在提交完Function接口的注释后，接下来是提交的都是他的实现类，抽象程度由高到低一层层的递进，非常有层次性。读完函数式相关接口，再去读其他类型的接口。

lambda表达式核心API:Function,supplier,Consumer,Predicate

```java
FunctionalInterface // 函数式接口
```

Function接口：这个接口定义的功能是：接收一个参数并返回一个结果(场景:类型转换,业务处理)

Consumer接口：有参数，没有返回值(场景:执行Callback)

Predicate接口：对给定的参数进行判断，返回值为true或者false(场景:过滤,对象比较)

一个典型的引用就是stream中的filter方法

```Java
Stream<T> filter(Predicate<? super T> predicate);
```

Supplier接口：没有输入，有返回值(场景:数据来源,代码替代接口)

在翻看JDK源码的时候，觉得有点迷糊，特别是对于Predicate接口，为什么这个接口给我的 感觉这么像断言（assert）呢？

带着疑问，去Google的时候，一片文章上贴了一段Stream的filter方法，我突然明白了:单独的去理解这些函数式接口是没有意义的,正是predicate接口的存在,才能实现filter方法.顺带的,我想到这么一句话,接口只是定义一个规范,定义功能,至于如何实现,得看下层实现类的定义.



lambda表达式出现的重要原因之一是:代替匿名内部类,简化代码

lambda表达式与函数式接口的关系:

在Java 8里面，**所有的Lambda的类型都是一个接口，而Lambda表达式本身，也就是”那段代码“，需要是这个接口的实现。**这是我认为理解Lambda的一个关键所在，简而言之就是，**Lambda表达式本身就是一个接口的实现**。

函数式接口:有且仅有一个抽象方法的接口就是函数式接口(细节见jdk源码)