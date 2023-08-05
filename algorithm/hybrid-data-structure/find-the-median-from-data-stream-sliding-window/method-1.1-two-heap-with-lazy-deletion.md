# Method 1.1 Two Heap with Lazy Deletion

There are usually two methods to do the lazy deletion:

* use a  map
* use a

## Summary

As we can see in the previous version, the delete function is very time-consuming. Lazy deletion can be used to improve performance.&#x20;

The basic idea is that:

* when an element is <mark style="color:orange;">supposed to be removed</mark>, we do not actually remove it from the heap immediately.&#x20;
* Instead, we <mark style="color:orange;">keep track of the elements to be deleted in a hash table</mark>. When an element at the top of the heap is supposed to be deleted, we then remove it.

Here is the code:

```java
class Solution {
    private int windowSize;
    private PriorityQueue<Integer> larger;
    private PriorityQueue<Integer> smaller;
    private HashMap<Integer, Integer> delayedRemovals; // not hash set since it might have same element
    private int smallerDelSize;
    private int largerDelSize;
    public double[] medianSlidingWindow(int[] nums, int k) {
        this.windowSize = k;
        this.smaller = new PriorityQueue<>(Collections.reverseOrder());
        this.larger = new PriorityQueue<>();
        this.delayedRemovals = new HashMap<>();
        double[] result = new double[nums.length - k + 1];
        for (int i = 0; i < nums.length; i++) {
            if (i >= k) { // delete start (k + 1)th, delete (i - k)th
                this.delete(nums[i - k]);
            }
            this.insert(nums[i]); // insert start 0th
            if (i >= k -1) { // record result start kth
                result[i - k + 1] = this.findMedian();
            }
        }
        return result;
    }
    private void insert(int num) {
        if (this.smaller.isEmpty() || num <= this.smaller.peek()) {
            this.smaller.offer(num);
        }
        else {
            this.larger.offer(num);
        }
        rebalance();
    }

    private void delete(int num){
        delayedRemovals.put(num, delayedRemovals.getOrDefault(num, 0) + 1);
        if (this.smaller.peek() >= num){
            this.smallerDelSize++;
        }
        else {
            this.largerDelSize ++;
        }
        while (!this.smaller.isEmpty() && delayedRemovals.containsKey(this.smaller.peek())) {
            delayedRemovals.put(smaller.peek(), delayedRemovals.get(this.smaller.peek()) - 1);
            if (delayedRemovals.get(this.smaller.peek()) == 0) {
                delayedRemovals.remove(this.smaller.peek());
            }
            this.smaller.poll();
            this.smallerDelSize--;
        }
        while (!this.larger.isEmpty() && delayedRemovals.containsKey(this.larger.peek())) {
            delayedRemovals.put(this.larger.peek(), delayedRemovals.get(this.larger.peek()) - 1);
            if (delayedRemovals.get(this.larger.peek()) == 0) {
                delayedRemovals.remove(this.larger.peek());
            }
            this.larger.poll();
            this.largerDelSize--;
        }
        rebalance();
    }
    private double findMedian() {
        if (this.smaller.size() == this.larger.size()) {
            return (double) this.smaller.peek() + this.larger.peek() /2.0;
        }
        else  {
            return (double) this.smaller.peek();
        }
    }
    private void rebalance() {
        int smallerSize = this.smaller.size() - this.smallerDelSize;
        int largerSize = this.larger.size() - this.largerDelSize;
        int size = smallerSize + largerSize;
        if (size % 2 == 0) {
            while (smallerSize != largerSize) {
                if (smallerSize > largerSize) {
                    this.larger.offer(this.smaller.poll());
                }
                else {
                    this.smaller.offer(this.larger.poll());
                }
            }
        }
        else {
            while (smallerSize!= this.larger.size() + 1){
                if (smallerSize > this.larger.size()) {
                    this.larger.offer(this.smaller.poll());
                }
                else {
                    this.smaller.offer(this.larger.poll());
                }
            }
        }
    }
}
```







