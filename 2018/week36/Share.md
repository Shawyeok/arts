## [Sizeof for java](https://blogs.oracle.com/sundararajan/sizeof-for-java)
在heapdump分析工具里面一般都会有显示对象的大小，那么有没有想过这个对象大小是如何被计算出来的呢？

我们知道在C语言中，有一个内置函数`sizeof`可以计算出指定对象占用的内存大小，但在java中严格意义上并没有提供这个函数，对象的大小也和具体运行的JVM实现有关系，同一个对象在32位和64位的虚拟机中占用的内存大小也不一样。但我们可以根据不同的虚拟机创建一个对应表，来记录对象头、数组头、引用等类型的内存占用大小，然后通过递归分别计算对象中所有成员变量的内存大小，将其加起来就是对象总共所占用的内存大小了。

然后JDK的开发团队已经帮我们完成这个事了，那就是`jdk.nashorn.internal.ir.debug.ObjectSizeCalculator#getObjectSize`

### 参考链接
- https://www.javaworld.com/article/2077408/core-java/sizeof-for-java.html
