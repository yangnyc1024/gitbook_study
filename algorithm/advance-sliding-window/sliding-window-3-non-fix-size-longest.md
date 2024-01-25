# Sliding Window 3 Non fix size longest

Template of Longset Problem

```java
int slow = 0;
int fast = 0;
[slow, fast]
while (fast < S.length()) {
    // 1. add S[fast] into the sliding window
    // 2. move slow to the correspoding position, update global min/max value;
    while (window not staisfes the property) {
        // 1. remove slow from the window
        slow++;
    }
    // here slow is the lestmost position satisfying the property
    // !! make sure you understand clearly about the termination of the while loop
    // 1. update global longest. [slow, fast]
    fast++;
}
```

fast:相当于是遍历

slow相当于是保证找到符合条件的

#### Q1 Find the longest substring withou duplciate characters



#### Q1.1 Given a string containing only lowercase English lettesr, how many of its substrings satisfy the requirement of 'containing duplicate characters'



#### Q2 Find the longest substring with at most k distinct characters.

```java
int slow = 0;
Map<Character, Integer> map = new HashMap<>();
int longest = Integer.MIN_VALUE;
for (int fast = 0; fast < input.length; fast++) {
    map.put(input[fast], map.getOrDefault(intput[fast], 0) + 1);
    while (map.size() > k) {
        Integer count = map.get(input[slow]);
        if (count == 1)  {
            countMap.remove(input[slow]);
        }
        else {
            map.put(input[slow] - 1);
        }
    }
    longest = Math.max(longest, fast - slow + 1);
}
return longest;
```





### Work with Stream





#### Q3 Desgin a counter class



常用design类似的题目

1. understand the requirements and use cases, assumptions
2. design the API -- public methods, define the input parameters, return values, corner case execptions
3. determin the member fields - internal states - access modifiers
4. implement APIs, decouple the internal logics with private method (helper methods)
5. implement the constructor - corner cases. initialize the member fields.

```java
class Counter{
    private Queue<Long> hits;
    public static final long RANGE = 5 *60 * 1000L;
    
    public Counter() {
        hits = new ArrayDeque<>();
    }
    void record() {
        long cur = System.currentMillis();
        evict(cur - RANGE);
        hits.offer(cur);
    } 
    long hitsLastFiveMins() {
        long cur = System.currentMillis();
        evict(cur - RANGE);
        raeturn hits.size();
    
    }
    private void evict(long target) {
        while(!hits.isEmpty() && hits.peek() < target) {
            hits.poll();
        }
    }
}
```
