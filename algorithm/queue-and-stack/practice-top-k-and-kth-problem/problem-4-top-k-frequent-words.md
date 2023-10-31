# Problem 4 Top K Frequent Words

模型拓展，我有一个复合item



```
class Item {
    int A;
    long B;
    String C;
    ....
}
```

我给你一个Collection of item, 我让你return出 Top K XXXX(Comparator怎么写)的item们



Step1: 统计词频==》 最经典Use Case

* Map\<String, Integer> freqMap: Key: Word, Value: Frequency

```java
public void countFrequency(String[] words, List<String> words) {
    Map<String, Integer> freqMap = new HashMap<>();
    for (String word: word){
        freqMap.put(word, freqMapa.getOrDefault(word, 0) + 1);
    }
}
```

Step 2: 方法论

* 如果你用的是MinHeap: online, 手握K size heap，扫描元素每次淘汰最差的
* 如果你用的是MaxHeap: offline, 全部放进去poll K次

举一反三的复合体和母体的区别， PriortyQueue里放的item要自己写comparator， 根据题目需要全部都是能用if else搞定的事情
