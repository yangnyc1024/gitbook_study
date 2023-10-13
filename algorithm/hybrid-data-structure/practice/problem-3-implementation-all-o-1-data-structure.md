# Problem 3 Implementation All O(1) data structure



### Summary&#x20;

* 这道不是让我们keep 时间顺序，这题是大小顺序
*   <mark style="color:blue;">变化量为1（因为你每次最多增加1）的顺序模型</mark>

    * <mark style="color:blue;">对单一Data的每一次操作，导致的变化量至多为1:2D的结构设计</mark>
    * 单向排列次序不一定是个consecutive的次序
    *   当走流程的时候，新来一个key，走掉一个key，对于node的操作有很复杂，很可能新增或者删除现有的ListNode

        Node - Node - Node\
        Freq2- Freq3 - Freq5



#### 横向链接

* DLL + Map
* 对于所有变化量为1的reference Node我们可以实现对数量排序 + 所有对reference operation O(1)

#### 纵向链接

* 对于同样横向属性的key，我们可以再做一个DLL+Map，也可以存一个collection(List, Map)

#### easy case

* 不需要任何的顺序， set/list

```java
// Some code
class Node{
    Node prev;
    Node next;
    // Collection of keys share the same row field
    Set<String> allStringShareSameFreq;
}
```

#### hard case

* 同样的频率的情况下，对另一个field再进行比较和存储，再观察是不是变量为1的顺序模型again，如果是的话，可以再来一个map2+ dll2,而dll2 inside of dll1

```java
// Some code
class Node{
    Node prev;
    Node next;
    // Store another DLL2
    AnotherOrderNode head;
    AnotherOrderNode tail
    // TreeMap, TreeSet
}
```

#### case even more

* 无限套娃



#### Middle Level：所有API走流程

* inc(String key)
* dec(String key)
* getMaxKey()
* getMinKey()

