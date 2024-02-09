# Deep Dive: PriorityQueue需要如何比较两个item(自己定义的/原本就有的)

## Summary

* 如果你本身就有自然序列/comparable，那么就写一个comparator<mark style="color:red;">（类 或者换comparator）</mark>
  * 可以共享定义
  * 可以一个定义有多个comparator
* 你创建一个新的，就自己写comparable(说白了comparable是他自己有的)



Method 1. Object 本身实现Comparable Interface: Override compareTo(E e) Method in Comparable interface

[https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)

Method 2: 实现Comparator Interface Override compare(E e1, E e2) Method in Comparator interface

[https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)

| 接口名                                                                                                                                                                              | 方法名                                                      |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| <p><mark style="color:blue;">interface Comparable&#x3C;E> {</mark></p><p>    <mark style="color:blue;">int compareTo(E ele);</mark></p><p><mark style="color:blue;">}</mark></p> | <mark style="color:blue;">int compareTo(T o)</mark>      |
| <p><mark style="color:red;">interface Comparator&#x3C;E> {</mark></p><p>    <mark style="color:red;">int compare(E o1, E o2);</mark></p><p><mark style="color:red;">}</mark></p> | <mark style="color:red;">int compare(T o1, T o2);</mark> |

## Method 1. Implementation Comparable

### Class 1: 原本就存在于Java中的的Object实现Comparable Interface

```java
// Some code

interface Comparable<E> {
    int compareTo(E ele);
}

class Integer implements Comparable<Integer> {
    private int value;
    public Integer(int value){
        this.value = value;
    }
    @Override
    public int compareTo(Integer another) {
        if (this.value == another.value) {
            return 0;
        }
        return this.value < another.value? -1: 1;
    }
}


// 例子
public static void main(String[] args){
    Integer one = new Integer(1);
    Integer two = new Integer(2);
    System.out.println(one.compareTo(two));
}
```

The return value of compareTo(another) method determines the order of this and another:\
0: this and another are of the same priority\
\-1(<0): this has higher priority than another\
1 (>0): this has less priority than another

CompareTo 的Return Value(int) 代表什么含义(this.compareTo(other))\
\- 0: this 和other的优先级相同（因为大小一样）\
\-1: this 小于other，因为this小，所以this优先\
1: this大于other，因为other小，所以other优先

### Class 2: 我们自己定义的Class Implement Comparable

```java
// Some code
class MyInteger implements Comparable<MyInteger> {
    private int value;
    public MyInteger(int value) {
        this.value = value;
    }
    @Override
    public int compareTo(MyInteger another) {
        if (this.equals(another)) {
            return 0;
        }
        return this.value > another.value ? -1: 1;
    }
    public static void main(String[] args) {
        PriorityQueue<MyInteger> minHeap = new PrirotyQueue<>();
        MyInteger myIntegerOne = new MyInteger(1);
        MyInteger myIntegerTwo = new MyInteger(2);
        minHeap.offer(new MyInteger(1));
        minHeap.offer(new MyInteger(2));
        int result = myIntegerOne.compareTo(myIntegerTwo); //1
        System.out.println("result" + result);
        System.out.println(minHeap.poll().value); //2
    }
}
```

## Method 2.实现Comparator Interface Override compare(E e1, E e2) Method in Comparator interface

Provide an extra Comparator object to compare the elements

```java
// Some code

interface Comparator<E> {
    int compare(E o1, E o2);
}

class MyInteger {
    public int value;
    public MyInteger(int value) {
        this.value = value;
    }
}

class MyComparator implements Comparator<MyInteger> {
    @Override
    public int compare(Cell o1, Cell o2) {
        if (o1.value == o2.value) {
            return 0;
        }
        return o1.value < o2.value ? -1: 1;
    }
}
public static void main(String[] args) {
    PriorityQueue<MyInteger> minHeap = new PriorityQueue<>(11, new MyComparator());
    MyInteger myIntegerOne = new MyInteger(1);
    MyInteger myIntegerTwo = new MyInteger(2);
    minHeap.offer(new MyInteger(1));
    minHeap.offer(new MyInteger(2));
    
    MyComparator myComparator = new MyComparator();
    int result = myComparator.compare(myIntegerOne, myIntegerTwo);
    System.out.println("result: " + result);
    System.out.println(minHeap.poll().value);
}
```

This is another interface Comparator, and it is used to compare two elements with the same type E.

```java
// Some code
interface Comparator<E> {
    int compare(E o1, E o2);
}
class Cell {
    public int row;
    public int col;
    public int value;
    public Cell(int row, int col, int value) {
        this.row = row;
        this.col = col;
        this.value = value;
    }
}
class MyComparator implements Comparator<Cell> {
    @Override 
    public int compare(Cell c1, Cell c2) {
        if (c1.value == c2.value) {
            return 0;
        }
        return c1.value < c2.value ? -1: 1;
    }

}
```



<mark style="color:purple;">**如何把这个Comaprator传进PriorityQueue？**</mark>

```java
// We want to have a minHeap by the value of the Cell elements
public static void main(String[] args) {
    PrirotyQueue<Cell> minHeap = new PriorityQueue<>(11, new MyComarator());
    Cell c1 = new Cell(0, 0, 0);
    Cell c2 = new Cell(0, 1, 2);
    minHeap.offer(c1);
    minHeap.offer(c2);
    MyComparator myComparator = new MyComparator();
    int result = myComparator.compare(c1, c2);
    System.out.println("result " + result);
    System.out.println(minHeap.poll().value);
}
```



## <mark style="color:purple;">**一些问题**</mark>



### Question 1 有咩有可能一个类已经实现了Comarable， 那这个时候我能写这个Class的Comaprator吗？

可以： 语义

你说1 比2小，我不同意，在我这1就比2大

```java
// Some code
class ReverseComaprator implements Comparator<Integer> {
    @Override
    public int compare(Integer i1, Integer i2) {
        if (i1.equals(i2)) {
            return 0;
        }
        return i1 < i2 ? 1: -1;
    }
}

// Integer 类已经实现的Comparable
public static void main(String[] args) {
    Integer one = new Integer(1);
    Integer two = new Integer(2);
    System.out.println(one.comapreTo(two));
    ReverseComparator myComparator = new ReverseComparator();
    System.out.println(myComparator.compare(one, two));
}


// -1 这个compareTo的方法是来自于Comparable的
System.out.println(one.compareTo(two));

// 1 这个compare方法来自Comparator的
ReverseComparator myComparator = new ReverseComparator();
myComparator.compare(one, two)

```



### Question 2 如何让PriorityQueue 不按照Comparable的compare To来比较，而是用我们定义的Comparator的compare来比较呢？

```java
// Some code

PriortyQueue<Integer> minHeap = new PriorityQueue<>();
PriortyQueue<Integer> newMinHeap = new PriorityQueue<>(16, new ReverseComparator());


public static void main(String[] args) {
    PriortyQueue<Integer> mimHeap = new PriortyQueue<>();
    PriortyQueue<Integer> newMinHeap = new PriortyQueue<>(16, new ReverseComparator());
    minHeap.offer(1);
    minHeap.offer(2);
    mimHeap.offer(3);
    minHeap.offer(4);
    minHeap.offer(5);
    while (!minHeap.isEmpty()) {
        System.out.println("minHeap element:" + minHeap.poll());
    }
    newMinHeap.offer(1);
    newMinHeap.offer(2);
    newMinHeap.offer(3);
    newMinHeap.offer(4);
    newMinHeap.offer(5);
    while (!newMinHeap.isEmpty()) {
        System.out.println("newMinHeap element: " + newMinHeap.poll());
    }
}
```



### Question 3: 那这样，叫minHeap还合适吗？<mark style="color:red;">那怎么创建maxHeap</mark>

* 用新建comparator
* Collections.reverseOrder()?

#### Method 1:可以自己建立一个Comparator 让比较大的元素优先级高，传进PriortyQueue

```java
// Some code
PriorityQueue<Integer> minHeap = new PriortyQueue<Integer>();
// I would like to have a max heap here
// So I need to provide a new Comparator, 
// The ordering defined by the Comparator is the reversed natural order provided by Integer class

class ReverseComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer i1, Integer i2) {
        if (i1.equals(i2)) {
            return 0;
        }
        return i1 < i2 ? 1: -1;
    }
}
public static void main(String[] args) {
    PriortyQueue<Integer> maxHeap = new PriortyQueue<>(16, new RevereseComparator());
    maxHeap.offer(4);
    maxHeap.offer(5);
    maxHeap.offer(2);
    maxHeap.offer(3);
    maxHeap.offer(1);
    while (!maxHeap.isEmpty()) {
        System.out.println(maxHeap.poll());
    }
}
```

#### Method 2:用Utility Method

* 第二类可以用Collections.reverseOrder()
* 本质： reverseOrder()这个方法本质上返回了一个Comparator(是一个instance)，所以其实把Collections.reverseOrder()传进PriorityQueue相当于传进一个Comparator

```java
// Some code
PriorityQueue<Cell> maxHeap = new PriorityQueue<cell>(Collection.reverseOrder());
```

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 2.04.41 PM.png" alt=""><figcaption></figcaption></figure>

* 如果这个Item自己也实现了Comparable, 你同时也传进来Comparator的话，PriorityQueue会按照Comparator来比较。
  * If E already implements Comparable\<E>, but you still provide a Comparator, PriorityQueue will choose the order specified in Comparator.



### Question 4: 怎么有的PriorityQueue Constructor建立的时候要传数字（16），有的可以 传reverseOrder()，到底有多少种Constructor

* 注意the inital capacity has to be >0;
* most frequently used constructors of PriorityQueue

| Requirement                                     | Constructors                                                                     |
| ----------------------------------------------- | -------------------------------------------------------------------------------- |
| class Cell must implement Comparable\<Cell>     | new <mark style="color:red;">PriorityQueue\<Cell>()</mark> (default capacity 11) |
| class Cell must implement Comparable\<Cell>     | new <mark style="color:red;">PriorityQueue\<Cell>(16)</mark>                     |
| class MyComparator implements Comparator\<Cell> | new <mark style="color:red;">PriorityQueue\<Cell>(16, new MyComparator())</mark> |
| class MyComparator implements Comparator\<Cell> | <mark style="color:red;">PriorityQueue\<Cell>(new MyComparator())</mark>         |

* if k < = 0, IllegalArgumentExpection will be thrown in the constructor. （k之前的16&11）

### Question 5: 我记得有个方法就是把一个Collection变成一个Heap的方法叫做Heapify并且是O(n) 的，但是为啥在java doc里找不到

* 注意，只能是传进去是collections，且必须要是自然序列
* 所以不能给collection+ compartor且用heapify
* 范型？将来可以放入任意类型？extend E

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-03 at 12.12.42 AM.png" alt=""><figcaption></figcaption></figure>



### Question 6: 还是看不懂？

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 2.16.55 PM.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 2.17.36 PM.png" alt=""><figcaption></figcaption></figure>

* 不是new  interface，而是创建类，且创建类interface。。。
* Static nested class VS non-static class
  * belong to class, or belong to instance
* Nest Class VS Inner Class
  * static nested class
    * a nested class associated with the outside class
    * can access class variables and method
  * inner class
    * a nested class associated with an instance of the class
    * can access instance variables and methods
  * anonymous class: nested class with no name
    * often replaceable by lambda expressions in Java 8

### Question 6b: 五种version出现

* Nested class vs inner class(无需知道。。。)
* 直接在外面写
* 不写？
* 写inner class
* lambda expression



#### Basic Version 1: 本来应该这样：亚古兽

```java
// Some code
class ReverseComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer i1, Integer i2) {
        if (i1.equals(i2)) {
            return 0;
        }
        return i1 < i2 ? 1: -1;
    }
}
PriorityQueue<Integer> maxHeap = new PriortyQueue<Integer>(16, new ReverseComparator());
```

#### Basic Version 1.5： 不想完整写一个Class: Static Nest Class

```java
// Some code
class MyInteger {
    public int value;
    public MyInteger(int value) {
        this.value = value;
    }
    static class MyComparator implements Compartor<MyInteger> {
        @Override
        public int compare(MyInteger o1, MyInteger o2){
            if (o1.value == o2.value) {
                return 0;
            }
            return o1.value > o2.value ? -1 : 1;
        }
    
    }
}


PriorityQueue<MyInteger> pq = new PriorityQueue<MyInteger>(new MyInteger.MyComparator());

public static void main(String[] args) {
    PriorityQueue<MyInteger> maxHeap = new PriortyQueue<>(new MyInteger.MyComparator());
    maxHeap.offer(new MyInteger(4));
    mayHeap.offer(new MyInteger(5));
    maxHeap.offer(new MyInteger(2));
    maxHeap.offer(new MyInteger(3));
    maxHeap.offer(new MyInteger(1));
    while (!maxHeap.isEmpty()) {
        System.out.println(maxHeap.poll().value);
    }
}

```

#### 进化Version 2: 你别那么麻烦，如果你只是用一给，用这一次就是为了给我PriortyQueue里面传进来一个，那么没有必要定一个class，可以定一个没有名字，匿名内部类。重点在于告诉我们里面那个comapre方法长什么样子就可以了

```java
// Some code
PriorityQueue<Integer> maxHeap = new PrirorityQueue<>(16, 
    new Comparator<Integer>() {
        @Override
        public int compare(Integer i1, Integer i2) {
            if (i1.equals(i2)) {
                return 0;
            }
            return i1 < i2 ? 1: -1;
        }
    }
);
```

new了一个匿名类（没有名字的）Comparator这个interface的实现类，里面的方法我给你了如下

```java
// Some code
@Override
public int compare(Integer i1, Integer i2) {
    if (i1.equals(i2)) {
        return 0;
    }
    return i1 < i2 ? 1: -1;
}
```

#### 进化 Version 3: Lambda Expressions

```java
// Some code
PriortyQueue<Integer> maxHeap = new PriorityQueue<>(
    (Integer i1, Integer i2) ->  {
    if (i1.equals(i2)) {
       return 0;
     }
     return i1 < i2 ? 1: -1;
     }
);
```

#### 进化 Version 4

```java
// Some code
// Declaration 1: 
PriortyQueue<MyInteger> maxHeap = 
new PriorityQueue<>((s1, s2) -> s1.value < s2.value? 1: s1.value > s2.value ? -1 : 0);
// Declaration 2:
PriortyQueue<MyInteger> maxHeap = 
new PriorityQueue<>((s1, s2) -> Integer.valueOf(s2.value).compareTo(s1.value));
// Declaration 3:
PriortyQueue<MyInteger> maxHeap = 
new PriorityQueue<>((s1, s2) -> Integer.compare(s2.value, s1.value));

```

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-03 at 12.39.06 AM.png" alt=""><figcaption></figcaption></figure>
