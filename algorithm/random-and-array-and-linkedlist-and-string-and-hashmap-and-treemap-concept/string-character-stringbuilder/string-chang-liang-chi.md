# String常量池

## What is String常量池？

The Java String constant pool is a special memory area within the Java Virtual Machine(JVM) where string literals (constants) are shored. It is a mechanism used by Java to optimize memory usage and improve performance when working with strings.



## Why?

* Memory Efficiency
* Performance Optimization
* String Immutability Guarantee



## 字符串创建的方法有以下三种

* 直接赋值法
  * 这种方式创建的字符串对象，只会在常量池中。返回的也只是字符串常量池中的对象引用
* new关键字
  * 这种方式会保证常量池和堆中都有这个对象，最后返回堆内存重的对象引用
* intern方法
  * 当调用intern方法时，如果池中已经包含一个与该String确定的字符串相同equals(Object)的字符串，则返回该字符串。否则，将此String对象添加到池中，饼返回此对象（原有）的引用



String真的不能改么？ 反射机制
