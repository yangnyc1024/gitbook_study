# Hash 底层

### What is hashMap?

* Array and LinkedList的一次重要的结合， HashMap
  * hash一个字符串，hash任意一个object会得到一个数字（hashCode）
* Map的底层本质：Array of LinkedList

### What is hash function?

* hash function
  * input: object
  * output: number
* good hash function
  * 不存在放进两个不同的object得到同一个number

### How to implement it?

* A table of buckets(an array of buckets), using the array index to denote each bucket
* for each \<key, value>, it goes to one of the buckets, the bucket index is determined by a hash function applied to the key and the size of the array

### Hash的步骤

* 将输入的元素转换为一串唯一的整数值
* 将整数值对童的数量取模将该整数值转换为桶的index，即index = x mod n
* 将元素储存在与该index对应的桶中

### Collision Control

* 当两个元素使用同一个hash函数映射到同一个位置（index）时，就会发生冲突。
* 为了解决这个问题，需要使用collision control技术
* 比如说seperate chaining（链式储存）和open addressing（开放地址探测）

#### Separate Chaining

* 如果发生碰撞，元素将被添加到桶中的链表中
* 这个链表时按照添加顺序添加和维护的，因此对于LinkedList的操作比对于HashSet的操作押送满
* 在极少数的情况下，所有的元素都被散列在到同一个桶里，这将导致性能下降到O(n)的级别

#### Open Addressing

* 当发生碰撞时，元素将尝试在桶中查询下一个可用的bucket。有三种重要的方法：
* 注意，放进去用的哪种方法，查找的时候也要用同一种方法
  * 线性探测(Linear Probing)： 在发生碰撞时，元素将尝试在桶的下一个位置查找可用的bucket。如果下一个位置也被占用了，它会继续寻找下一个，直到找到空的bucket
  * 二次探测(Quadratic Probing)：在发生碰撞时，元素将尝试在桶中查找可用的bucket。如果该位置被占用，则它将尝试在桶中，查找下一个位置，该位置时原始哈希位置加上1的平方。如果该位置被占用，则寻找下一个
  * 双重散列(Double Hashing)：在发生碰撞的时候，元素将尝试在桶中查找可用的buckted。他将使用另一个哈希函数来确定下一个位置的偏移量。这个过程将继续下去，直到一个空的buckted被找到为止

### Rehashing, Load factor, Capacity

* Rehashing: 当HashMap中的元素数量超过一定Load factor（负载因子）时，HashMap需要扩容。
  * 这涉及到创建一个新的桶数组，并将所有元素从旧数组rehash到新数组中。
  * 这操作可能会很昂贵，因此选择一个良好的负载因子（load factor）来最小调整大小的次数非常重要
* Load factor（负载因子）：负载因子确定HashMap需要调整大小的点。
  * 较高的负载因子意味着更少的调整大小，但也意味着更多的碰撞和更长的桶链。
  * 较低的负载因子意味着更多的调整大小，但也意味着更少的碰撞和更短的桶链。
  * Java默认的Load factor值时0.75（e.g. map里的entry数/桶数 《= 0.75）
* Capacity（容量）：HashMap的容量时它可以容纳的桶数。选择足够大的容量以避免频繁调整大小非常重要，但是也不要太大以免浪费内存

### ==， equals()， hashcode()

\==

* 确定两个primitive types是否具有相同的值
* 确定两个references是否指向相同的jobjects

equals()， hashcode()

* 定在Object类中，Object是java类的根类
* 任何java类都隐式地扩展Object类，因此如果在子类里面没有重写这两个方法，他就会继承Object类中的定义的内容
* equals()默认实现是检查两个referecne是否指向相同的对象"=="，即内容是否相等

Java中的==和equals，前者比较两个Objects的reference是否相等，后者比较两个objects的内容是否相等，而hashcode方法则用来计算key的hash值，进而决定这个key应该落在哪个桶里面。

因此，在实现自定的Object为key时，需要同时重写equals和hashcode方法，否则会2出现相同的key被多次添加到集合中的情况，以保证hashset和hashmap的正确使用。

```java
import java.util.HashSet;
import java.util.Set;


class Person {
    private String name;
    private int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (!(obj instanceof Person)) return false;
        Person person = (Person) obj;
        if (this.age != person.age) return false;
        return (name != null ? name.equals(person.name) : null) && (this.age == person.age);
    }
    @Override
    public int hashCode() {
        return 31* name.hashCode() + 31 * 31 * age;
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Harry", 18);
        Person p2 = new Person("Harry", 18);
        Set<Person> set = new HashSet<>();
        set.add(p1);
        set.add(p2);
    }

}
```

