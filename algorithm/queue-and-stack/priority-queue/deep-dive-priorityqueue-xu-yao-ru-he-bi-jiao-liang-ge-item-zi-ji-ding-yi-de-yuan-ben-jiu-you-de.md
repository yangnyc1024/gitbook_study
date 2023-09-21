# Deep Dive: PriorityQueue需要如何比较两个item(自己定义的/原本就有的)

## Summary

* 如果你本身就有自然序列/comparable，那么就写一个comparator<mark style="color:red;">（类 或者换comparator）</mark>
  * 可以共享定义
  * 可以一个定义有多个comparator
* 你创建一个新的，就自己写comparable(说白了comarable是他自己有的)



Method 1. Object 本身实现Comparable Interface: Override compareTo(E e) Method in Comparable interface

[https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)

Method 2: 实现Comparator Interface Override compare(E e1, E e2) Method in Comparator interface

[https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)

| 接口名                                                                              | 方法名                      |
| -------------------------------------------------------------------------------- | ------------------------ |
| <p>interface Comparable&#x3C;E> {</p><p>    int compareTo(E ele);</p><p>}</p>    | int compareTo(T o)       |
| <p>interface Comparator&#x3C;E> {</p><p>    int compare(E o1, E o2);</p><p>}</p> | int compare(T o1, T o2); |

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

<mark style="color:red;">注意看代码！！！</mark>



## Question 1 有咩有可能一个类已经实现了Comarable， 那这个时候我能写这个Class的Comaprator吗？





## Question 2 如何让PriorityQueue 不按照Comparable的compare To来比较，而是用我们定义的Comparator的compare来比较呢？





## Question 3: 那这样，叫minHeap还合适吗？那怎么创建maxHeap

* 用新建comparator
* Collections.reverseOrder()?





<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 2.04.41 PM.png" alt=""><figcaption></figcaption></figure>

* 第二类可以用Collections.reverseOrder()





## Question 4: 怎么有的PriorityQueue Constructor建立的时候要传数字（16），有的可以 传reverseOrder()，到底有多少种Constructor

* 注意theinital capacity has to be >0;



## Question 5: 我记得有个方法就是把一个Collection变成一个Heap的方法叫做Heapify并且是O(n) 的，但是为啥在java doc里找不到

* 注意，只能是传进去是collections，且必须要是自然序列
* 所以不能给collection+ compartor且用heapify
* 范型？将来可以放入任意类型？extend E





## Question 6: 还是看不懂？

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 2.16.55 PM.png" alt=""><figcaption></figcaption></figure>

* 不是new  interface，而是创建类，且创建类interface。。。



Nested class vs inner class(无需知道。。。)

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 2.17.36 PM.png" alt=""><figcaption></figcaption></figure>

## Question 6b: 五种version出现

* 直接在外面写
* 不写？
* 写inner class
* lambda expression