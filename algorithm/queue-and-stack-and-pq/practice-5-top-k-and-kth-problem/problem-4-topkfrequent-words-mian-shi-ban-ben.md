# Problem 4 Top K Frequent Words面试版本

````java
// Some code

```java
/*
1) build new class with freq, and word
2) put the first k new elements 
3) check the rest quanlified candidate(freq > container.smallest) and put into the container
*/

class Solution {
    // class WordInfo implements Comparable<WordInfo>{
    class WordInfo {
        int freq;
        String word;
        public WordInfo(String word, int freq) {
            this.word = word;
            this.freq = freq;
        }
        // @Override
        // public int compareTo(WordInfo that) {
        //     int result = Integer.compare(this.freq, that.freq);
        //     int result_1 = that.word.compareTo(this.word);
        //     if (result == 0) return result_1;
        //     return result;
        // }
    }
    public List<String> topKFrequent(String[] words, int k) {
        // sanity check
        List<String> result = new ArrayList<>();
        if (words == null || k <= 0) {
            return result;
        }
        // build this new container
        PriorityQueue<WordInfo> minHeap = new PriorityQueue<>((e1, e2) -> {
            if (Integer.compare(e1.freq, e2.freq) == 0) return e2.word.compareTo(e1.word);
            return Integer.compare(e1.freq, e2.freq); 
            }
        );
        Map<String, Integer> wordsFreq = buildFreq(words);
        
        // put all in, when after kth check if it is satisfied the candidate condition
        for (String eachWord: wordsFreq.keySet()) {
            minHeap.offer(new WordInfo(eachWord, wordsFreq.get(eachWord)));
            if (minHeap.size() > k) {
                minHeap.poll();
            }

        }
        // output
        while (!minHeap.isEmpty()) {
            result.add(minHeap.poll().word);
        }
        Collections.reverse(result);
        return result;
    }
    private Map<String, Integer> buildFreq(String[] words) {
        Map<String, Integer> map = new HashMap<>();
        for (String word: words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }
        return map;
    }
}
```
````
