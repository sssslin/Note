需要首先弄清楚的问题:

spring最核心的两块内容IOC和AOP

spring boot启动过程是什么?







相对次要的问题:

dubbo了解多少?

Java 8 stream API的性能



单例模式

最简单的单例模式如何实现：（静态内部类的）

1.一个用于初始化静态final实例的静态内部类

2.一个private的构造方法

3.一个public的获取实例方法

示例代码如下：

```java
public class SingleTon{
    
  private SingleTon(){}

  private static class SingleTonHoler{
     private static SingleTon INSTANCE = new SingleTon();
  }

  public static SingleTon getInstance(){
    return SingleTonHoler.INSTANCE;
  }
  ...
}
```

 静态内部类的优点是：外部类加载时并不需要立即加载内部类，内部类不被加载则不去初始化INSTANCE，故而不占内存。即当SingleTon第一次被加载时，并不需要去加载SingleTonHoler，只有当getInstance()方法第一次被调用时，才会去初始化INSTANCE,第一次调用getInstance()方法会导致虚拟机加载SingleTonHoler类，这种方法不仅能确保线程安全，也能保证单例的唯一性，同时也延迟了单例的实例化





