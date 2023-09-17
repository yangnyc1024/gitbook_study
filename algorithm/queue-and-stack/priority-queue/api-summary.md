# API Summary



## API 1: add(E e)



## API 2: offer(E e)



Answer: the offer() and add() methods are actually a bit different for capacity-constrained queues, but in the case of PriortyQueue, both are the same.(在priorityqueue里都一样，用offer就好)



## API 3: peek()

* 所有的数据结构，都要避免从空的data stucture里拿元素(pq.isEmpty())



## API 4: poll()





## API 5: remove()

* 不一定是O(n)

## API 6: remove(Object o)



## API 7: size()



## API 8: clear()





## API 9: comparator()

<mark style="color:red;">代码？</mark>

```java
// Some code
public static void main(String[] args) {
    PrirotyQueue<String> minHeap1 = new PriorityQueue<>();
    Comparaator<? super String> comparator1 = minHeap1.comparator();
    
} 
```



## API 10: contains(Object o)

* 这个是O(n)



## API 11: isEmpty()



## API 12: toArray()

* 返回的是Object\[]

<mark style="color:red;">代码？</mark>



