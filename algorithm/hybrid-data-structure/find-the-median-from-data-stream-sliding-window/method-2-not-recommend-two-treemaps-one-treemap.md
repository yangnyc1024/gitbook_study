---
description: Map
---

# Method 2(not recommend) Two TreeMaps/ One TreeMap

You can indeed solve the sliding window median problem using two `TreeSet`s. In this case, `TreeSet` is particularly suitable because it supports the removal of arbitrary elements in logarithmic time, which is better than `PriorityQueue` in this case.

* One thing to keep in mind is that duplicate elements can exist in the sliding window, so we cannot simply use two `TreeSet`s.&#x20;
* Instead, we can use two `TreeMap`s, where the <mark style="color:blue;">key is the element</mark> and <mark style="color:blue;">the value is the frequency of the element</mark>.&#x20;
* `TreeMap` is sorted, so we can use it like a `TreeSet` that also supports duplicate elements.

基本上意思就是说，既然没法区分，那就合在一起处理

* 相当于比如说我们有两个value2，
  * 一种是用treeSet，记录elements
    * element 1: value 2，index 1，
    * element 2: value 2， index 2
  * 或者直接用treeMap，记录\<value 2，2个>&#x20;

但这题如果用treeMap在rebalance上会比较复杂，因为有重复的value会导致两个data strcuture计数上的问题，以下是leetcode的参考答案之一



````java
```java
class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {
        if (nums == null) return new double[]{};
        int len = nums.length;
        double[] ret = new double[len - k + 1];
        FindMedian queue = new FindMedian(k);
        for (int i = 0; i < len; i++) {
            if (queue.size() == k) {
                //System.out.println("removed" + (i-k));
                queue.remove(nums[i - k]);
            }
            queue.add(nums[i]);
            if (queue.size() == k) {
                //System.out.println("ret index: " + (i-k+1));
                ret[i - k + 1] = queue.getMedian();
            }
        }
        return ret;
    }

    private class FindMedian {
        public TreeMap<Integer, Integer> tree1;
        public TreeMap<Integer, Integer> tree2;
        public int size1, size2, k, kk;

        public FindMedian(int k){
            tree1 = new TreeMap<Integer, Integer>();
            tree2 = new TreeMap<Integer, Integer>();
            this.k = k;
            size1 = 0;
            size2 = 0;

            if (k % 2 != 0) {
                kk = k + 1;
            } else {
                kk = k;
            }
        }

        public void add(int n) {
            if(tree1.containsKey(n)) {
                tree1.put(n, tree1.get(n) + 1);
            } else {
                tree1.put(n, 1);
            }
            size1++;
            selfBalancing();
        }

        public double getMedian() {
            double median = 0.0;

            if (k % 2 != 0) {
                if (size1 != 0) {
                    median = (double)tree1.lastKey();
                }
            } else {
                if (size1 != 0 && size2 != 0) {
                    median = ((double)tree1.lastKey() + (double)tree2.firstKey()) / 2;
                } else {
                    throw new IllegalArgumentException("not a right time to use getMedian");
                }
            }
            return median;
        }

        public void remove(int n) {
            if (tree1.containsKey(n)) {
                if (tree1.get(n) > 1) {
                    tree1.put(n, tree1.get(n) - 1);
                } else {
                    tree1.remove(n);
                }
                size1--;
                selfBalancing();
            } else if (tree2.containsKey(n)) {
                if (tree2.get(n) > 1) {
                    tree2.put(n, tree2.get(n) - 1);
                } else {
                    tree2.remove(n);
                }
                size2--;
                selfBalancing();
            }
        }

        public int size(){
            return size1 + size2;
        }

        public void selfBalancing() {
            while (size1 < kk / 2 && size2 > 0) {
                Integer smallestInTree2 = tree2.firstKey();
                if (tree2.get(smallestInTree2) > 1) {
                    tree2.put(smallestInTree2, tree2.get(smallestInTree2) - 1);
                } else {
                    tree2.remove(smallestInTree2);
                }
                if (tree1.containsKey(smallestInTree2)) {
                    tree1.put(smallestInTree2, tree1.get(smallestInTree2) + 1);
                } else {
                    tree1.put(smallestInTree2, 1);
                }
                size1++;
                size2--;
            }
            while (size1 > kk / 2) {
                Integer largestInTree1 = tree1.lastKey();
                if (tree2.containsKey(largestInTree1)) {
                    tree2.put(largestInTree1, tree2.get(largestInTree1) + 1);
                } else {
                    tree2.put(largestInTree1, 1);
                }
                if (tree1.get(largestInTree1) > 1) {
                    tree1.put(largestInTree1, tree1.get(largestInTree1) - 1);
                } else {
                    tree1.remove(largestInTree1);
                }
                size2++;
                size1--;
            }
            if (size1 == kk / 2) {
                while (!tree2.isEmpty() && tree1.lastKey() > tree2.firstKey()) {
                    Integer largestInTree1 = tree1.lastKey();
                    Integer smallestInTree2 = tree2.firstKey();
                    if (tree2.get(smallestInTree2) > 1) {
                        tree2.put(smallestInTree2, tree2.get(smallestInTree2) - 1);
                    } else {
                        tree2.remove(smallestInTree2);
                    }
                    if (tree1.get(largestInTree1) > 1) {
                        tree1.put(largestInTree1, tree1.get(largestInTree1) - 1);
                    } else {
                        tree1.remove(largestInTree1);
                    }
                    if (tree1.containsKey(smallestInTree2)) {
                        tree1.put(smallestInTree2, tree1.get(smallestInTree2) + 1);
                    } else {
                        tree1.put(smallestInTree2, 1);
                    }
                    if (tree2.containsKey(largestInTree1)) {
                        tree2.put(largestInTree1, tree2.get(largestInTree1) + 1);
                    } else {
                        tree2.put(largestInTree1, 1);
                    }
                }
            }
        }
    }
}
```
````

