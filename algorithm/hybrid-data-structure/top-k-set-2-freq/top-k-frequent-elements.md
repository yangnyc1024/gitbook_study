---
description: https://leetcode.com/problems/top-k-frequent-elements/
---

# Top K Frequent Elements

#### Method 1 PriorityQueue + HashMap

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
    // step 1: build the hashmap
        Map<Integer, Integer> map = new HashMap<>();
        // map, key: value, index: freq
    // step 2: build the minHeap
        PriorityQueue<Element> minHeap  = new PriorityQueue<>();
        // go over all the element in hashmap
        for (int i = 0; i < nums.length; i++) { // not for all, only for heap
            if (map.containsKey(nums[i])) {
                map.replace(nums[i] , map.get(nums[i]) + 1);
            }
            else {
                map.put(nums[i], 1);
            }
        }
    // step 3: for loop put in
        for (int key : map.keySet()) {
            minHeap.offer(new Element(key, map.get(key)));
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

    // step 4: print all the element in the current heap 
        int[] ret = new int[k];
        for(int i = 0; i < k; i++){
            ret[i] = minHeap.poll().value;
        }
        
        return ret;
    }

    class Element implements Comparable<Element> {
        Integer value;
        Integer freq;
        public Element(Integer value, Integer freq) {
            this.value = value;
            this.freq = freq;
        }
        public int compareTo(Element that) {
            if (this.freq == that.freq) {
                return 0;
            }
            return this.freq < that.freq ?  -1 : 1;
        }
    }
}
```

#### Method 2 TreeSet + HashMap

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // sanity check

        int[] result = new int[k];
        Map<Integer, Integer> lookUp = new HashMap<>();
        // build the look up map, <value, freq>
        for (int i = 0; i < nums.length; i++) {
            lookUp.put(nums[i], lookUp.getOrDefault(nums[i], 0) + 1);
        }

        TreeSet<Element> treeSet= new TreeSet<>();
        for (Integer value: lookUp.keySet()) {
            Element cur = new Element(value, lookUp.get(value));
            treeSet.add(cur);
        }
        for (int i = k - 1; i >= 0; i--) {
            result[i] = treeSet.pollLast().value;
        }
        return result;
    }
    class Element implements Comparable<Element> {
        int value;
        int freq;
        public Element(int value, int freq) {
            this.value = value;
            this.freq = freq;
        }
        @Override
        public int compareTo(Element that) {
            int result = Integer.compare(this.freq, that.freq);
            if (result == 0) {
                return Integer.compare(this.value, that.value);
            }
            return result;
        }
    }
}
```



Question: double linkedlist做的了么？

