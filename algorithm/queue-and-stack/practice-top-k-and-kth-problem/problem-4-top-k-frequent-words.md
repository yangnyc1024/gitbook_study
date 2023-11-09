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





#### Method1: MinHeap

```java
//用新的class的version

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

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        LinkedList<String> result = new LinkedList<>();
        if (words == null || k< = 0) {
            return result;
        }
        Map<String, Integer> wordsFrequency = buildFrequency(words);
        PriorityQueue<Map.Entry(String, Integer)> minHeap = new PrirotyQueue<> (
            (e1, e2) -> {
                if (e1.getValue().equals.(e2.getValue())) {
                    return e2.getKey().compareTo(e1.getKey());
                }
                return Integer.compare(e1.getValue(), e2.getValue());
            }
        )
        for (Map.Entry(String, Integer) entry: wordsFrequency.entrySet()) {
            minHeap.offer(entry);
            if (minHeap.size() > k) {
                mimHeap.poll();
            }
        }
        while (!minHeap.isEmpty()) {
            return.addFirst(minHeap.poll().getKey());
        }
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



Method 2: MaxHeap

```java
// 不自己build Map Entry
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        List<String> result = new ArrayList<>();
        if (words == null || k <= 0) {
            return result;
        }
        Map<String, Integer> wordsFrequency = buildFrequency(words);
        PriorityQueue<Map.Entry<String, Integer>> maxHeap = new PriorityQueue<> (
            (e1, e2) -> {
                if (e1.getValue().equals(e2.getValue())) {
                    return e1.getKey().compareTo(e2.getKey());
                }
                return Integer.compare(e2.getValue(), e1.getValue());
            }
        );
        for (Map.Entry(String, Integer) entry: wordsFrequency.entrySet()) {
            maxHeap.offer(entry);
        }
        while (k > 0) {
            result.add(maxHeap.poll().getKey());
            k--;
        }
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

```java
// Some code


class Solution {
    class WordInfo { 
        String word;
        Integer frequency;
        public wordInfo(String word, Integer frequency) {
            this.word;
            this.frequency = frequency;
        }
    }
    public List<String> topKFrequent(String[] words, int k) {
        List<String> result = new ArrayList<>();
        // sanity check
        if (words == null || words.length == 0) {
            return result;
        }
        
        // build the freq Map,
        Map<String, Integer> wordsFrequency= buildMap(words);
        
        
        //  build the minHeap with element wordInfo
        PriortyQueue<WordInfo> maxHeap = new PriortyQueue<>(new Comparator<WordInfo>(){
            @Override
            public int compare(WordInfo word1, WordInfo  word2) {
                if (word1.frequency.equals(word2.frequency)) {
                    return word1.word.compareTo(word2.word);
                }
                return Integer.compare(word2.frequency, word1.frequency);
            }
        });
        
        
        // put all new wordInfo into heap
        for (String eachWord: wordsFrequency.keySet()) {
            maxHeap.offer(new WordInfo(eachWord, wordsFrequency.get(eachWord)));
        }    
        
        // poll all wordInfo out & put into the result list
        k = Math.min(k, maxHeap.size());
        while (k > 0) {
            result.add(maxHeap.poll().word);
            k--;
        }
        return result;
    }
    private Map<String, Integer> buildFrequency(String[] words) {
        Map<String. Integer> map = new HashMap<>();
        for (String word: words){
            int wordCount = map.getOrDefault(word, 0) + 1;
            map.put(word, wordCount);
        }
        return map;
    }
}
```
