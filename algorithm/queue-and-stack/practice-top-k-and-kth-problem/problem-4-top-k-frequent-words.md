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





#### Method: MinHeap

```java
class Solution {
    class WordInfo {
        String word;
        Integer frequency;
        public WordInfo(String word, Integer frequency) {
            this.word = word;
            this.frequency = frequency;
        }
    }

    class MyComparator implements Comparator<WordInfo> {
       @Overide
       public int compare(WordInfo word1, WordInfo word2) {
           if (word1.frequency.equals(word.frequency)) {
               return word2.word.compareTo(word1.word);
           }
           return Integer.compare(word1.frequency, word2.frequency);
       } 
    }
    public List<String> topKFrequent(String[] words, int k)  {
        List<String> result = new ArrayList<>();
        
        PriortityQueue<WordInfo> minHeap = new PriorityQueue(new Mycomparator());
        Map<String, Integer> wordsFrequency = buildFrequency(words);
        
        for (String eachWord: wordsFrequency.keySet()) {
            minHeap.offer(new WordInfo(eachWord, wordsFrequency.get(eachWord)));
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }
        while (!minHeap.isEmpty()) {
            result.add(minHeap.poll().word);
        }
        Collections.reverse(result);
        return result;
    }
    private Map<String, Integer> buildFrequency(String[] words) {
        Map<String, Integer> map = new HashMap<>();
        for (String word: words) {
            int wordCount = map.getOrDefault(word, 0) + 1;
            map.put(word, wordCount);
        }
        return map;
    }
}

```



