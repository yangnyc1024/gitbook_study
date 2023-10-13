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
  * case 1: 这个key是第一次出现
    * case1.1 看看有没有对应的freq =1 的node
      * 创建一个并且加入map +dll(set)
    * case1.2 如果已经存在在freq为1的弄的
      * 把这个新的data加入到已经存在的node set里面
  * case 2: 这个key不是第一次出现
    * 首先得知道他是第几次出现（map里面拿freq node）
    * 我们应该把这个node放到现在的freq+1的freq node
    * <mark style="color:blue;">这个freq + 1一定是你现在的freqNode.next么？</mark>
    * case2.1 不存在freq +1 的node
      * 创建一个freq + 1的freqNode并且把这个node插入到当前freqNode之后
      * 对应的key加入到这个你插入的freqNode里
    * case2.2 存在freq + 1的node
      * 对应的key加入到这个你插入的freqNode里
    * 不管存在不存在，现在key都不是freqNode里的人了，你得从freqNode里把这个key删除
      * <mark style="color:blue;">你现在把这个key当前的freqNode里删除之后，有没有可能当前的freqNode里就没有任何key了？</mark>
      * <mark style="color:orange;">如果空了，我们就要连着这个FreqNode + Map删除</mark>
* dec(String key)
  * case 1: 这个key是第一次出现
    * 直接return
  * case 2: 这个key不是第一次出现
    * 首先得知道他是第几次出现（map里面拿freq node）
    * 我们应该把这个node放到现在的freq+1的freq node
    * <mark style="color:blue;">这个key只出现了一次？我们不存在freq为0的FreqNode</mark>
      * 删除这个key + check freq为1的FreqNode是否需要删除
    * <mark style="color:blue;">这个freq - 1一定是你现在的freqNode.prev么？</mark>
    * case2.1 不存在freq - 1 的node
      * 创建一个freq - 1的freqNode并且把这个node插入到当前freqNode之前
      * 对应的key加入到这个你插入的freqNode里
    * case2.2 存在freq - 1的node
      * 对应的key加入到这个你插入的freqNode里
    * 不管存在不存在，现在key都不是freqNode里的人了，你得从freqNode里把这个key删除
      * <mark style="color:blue;">你现在把这个key当前的freqNode里删除之后，有没有可能当前的freqNode里就没有任何key了？</mark>
      * <mark style="color:orange;">如果空了，我们就要连着这个FreqNode + Map删除</mark>
* getMaxKey()
  * 从tailNode里随便拿一个
* getMinKey()
  * 从headNode里随便拿一个





```java
// Some code

public class AllOne {
    public AllOne() {
    
    
    }
    
    public void inc(String key) {
    
    }

    public void dec(String key) {
    
    }
    
    public String getMapKey() {
    
    
    }
    
    public String getMinKey() {
    
    }
    
    class FreqNode {
        int freq;
        Set<String> values; //二级结构里同享一个freq的所有string们
        FreqNode next;
        FreqNode prev;
        public FreqNode(int freq) {
            this.freq = freq;
            this.values = new HashSet<>();
            this.next = this.prev = null;
        }
    }
    private FreqNode insertNode(FreqNode current, int freq) {
        FreqNode newNode = new FreqNode(freq);
        FreqNode next = current.next;
        current.next = newNode;
        newNode.next = next;
        next.prev = newNode;
        newNode.prev = current;
        return newNode;
    }
    
    private FreqNode insertNode(FreqNode current, int freq) {
        FreqNode next = current.next;
        FreqNode prev = current.prev;
        prev.next = next;
        next.prev = prev;
        current.next = null;
        current.prev = null;
    }
}
```

