# Method 1.2 Two TreeSets



Note: How do we design delete(value) API, when we really would like to decide which one to delete

* Node{Value, sequence #} (assume we dont know the sequence?)
* Choice 1: remove the largest node with value 2 ==> treeSet.floor(new Node(2, globalCounter));
* Choice 2: remove the smallest node with value 2 ==> treeSet.ceiling(new Node(2, 0))

However, since this question is a sliding window, we can get the index



````java
class Solution {
    private int windowSize;
    private TreeSet<Element> smaller;
    private TreeSet<Element> larger;
    public double[] medianSlidingWindow(int[] nums, int k) {
        windowSize = nums.length;
        smaller = new TreeSet<>();
        larger = new TreeSet<>();
        double[] result = new double[nums.length - k + 1];
        for (int i = 0; i < nums.length; i++) {
            if (i >= k) {
                delete(nums[i - k], i - k);
            }
            add(nums[i], i);
            if (i >= k - 1) {
                result[i - k + 1] = findMedian();
            }
        }
        return result;
    }
    private void add(int num, int freq) {
        Element e = new Element(num, freq);
        if (smaller.isEmpty() || e.compareTo(smaller.last()) <= 0) {
            smaller.add(e);
        }
        else {
            larger.add(e);
        }
        rebalance();
    }
    private void delete(int num, int freq) {
        Element e = new Element(num, freq);
        if (smaller.contains(e)) {
            smaller.remove(e);
        }
        else {
            larger.remove(e);
        }
        rebalance();
    }
    private void rebalance() {
        while (smaller.size() > larger.size() + 1) {
            larger.add(smaller.pollLast());
        }
        while (larger.size() > smaller.size()){
            smaller.add(larger.pollFirst());
        }

    }
    private double findMedian() {
        if (this.smaller.size() == this.larger.size()) {
            return (double) this.smaller.last().value /2.0  + this.larger.first().value/ 2.0;
        }
        else {
            return (double) this.smaller.last().value;
        }
    }
    public class Element implements Comparable<Element> {
        int value;
        int index;
        public Element(int value, int index) {
            this.value = value;
            this.index = index;
        }
        @Override
        public int compareTo(Element that) {
            if (this.value != that.value) {
                return Integer.compare(this.value, that.value);
            }
            else {
                return Integer.compare(this.index, that.index);
            }
        }
    }
}
```
````
