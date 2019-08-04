# 面试题整理

1.一条链表,两个指针,如何确定是否存在环

该方法使用两个在链表中具有不同移动速度的指针。一旦它们进人环就会相遇，即表示存在环。这个判定方法的正确性在于，快速移动指针和慢速移动指针将会指向同一位置的唯一可能情况，就是整个或者部分链表是一个环。



2.Java类的加载过程(默认以HotSpot JVM作为基准)

(个人观点，市面上很多的很多参考资料有个比较明显的缺陷是，不结合源码来说明类的加载过程，从jdk到openJDK，垂直结构中是如何调用的)

类加载的过程本质是一个将一个类加载到内存中的过程,来源可以是本地磁盘上的class文件也可以是网络等渠道

加载(参考jdk8中的java.lang.ClassLoader)-验证-准备-解析-初始化-使用-卸载

```java
 protected Class<?> loadClass(String name, boolean resolve)
        throws ClassNotFoundException
    {
        synchronized (getClassLoadingLock(name)) {
            // First, check if the class has already been loaded
            Class<?> c = findLoadedClass(name);
            if (c == null) {
                long t0 = System.nanoTime();
                try {
                    if (parent != null) {
                        c = parent.loadClass(name, false);
                    } else {
                        c = findBootstrapClassOrNull(name);
                    }
                } catch (ClassNotFoundException e) {
                    // ClassNotFoundException thrown if class not found
                    // from the non-null parent class loader
                }

                if (c == null) {
                    // If still not found, then invoke findClass in order
                    // to find the class.
                    long t1 = System.nanoTime();
                    c = findClass(name);

                    // this is the defining class loader; record the stats
                    sun.misc.PerfCounter.getParentDelegationTime().addTime(t1 - t0);
                    sun.misc.PerfCounter.getFindClassTime().addElapsedTimeFrom(t1);
                    sun.misc.PerfCounter.getFindClasses().increment();
                }
            }
            if (resolve) {
                resolveClass(c);
            }
            return c;
        }
    }
```

3.mysql 有多少种连接方式

inner join(内连接)、left join(左连接),right join(右连接), cross join(交叉连接), full join(全链接,mysql不支持)



4.having子句和where子句的区别在哪

A:执行顺序上: where > 聚合函数(sum,min,max,avg,count) >  having

​    	    作用:where子句的作用是在过滤掉不符合条件的数据

​     having子句的作用是筛选满足条件的数据,条件中经常包含聚合函数



5.hashmap是一种怎么样的数据结构,如何处理hash碰撞

参考链接：<https://juejin.im/post/5aa5d8d26fb9a028d2079264#heading-14>

（疑点解答：key-value是成对存储的）

具体结构见hashmap:line 279:Node<K,V>,这个结构就是存储真正key,value的entry,jdk1.7类名为Entry(只是类名不同)

通过:链地址法

hashmap中调用hashCode()来计算hash值，由于不同的Java对象可能会出现一样的hash值，所以会导致hash冲突