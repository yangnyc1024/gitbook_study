# Method 1 Two Heap



{% code overflow="wrap" lineNumbers="true" fullWidth="true" %}
```java
class Solution {
    private int windowSize;
    private PriorityQueue<Integer> larger;
    private PriorityQueue<Integer> smaller;
    public double[] medianSlidingWindow(int[] nums, int k) {
        this.windowSize = k;
        this.smaller = new PriorityQueue<>(Collections.reverseOrder());
        this.larger = new PriorityQueue<>();
        double[] result = new double[nums.length - k + 1];
        for (int i = 0; i < nums.length; i++) {
            if (i >= k) { // delete start (k + 1)th
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
        if (num <= this.smaller.peek()) {
            this.smaller.remove(num);
        }
        else {
            this.larger.remove(num);
        }
        rebalance();
    }
    private double findMedian() {
        if (this.smaller.size() == this.larger.size()) {
            return (double) smaller.peek()/2.0 + larger.peek() /2.0;
        }
        else  {
            return (double)smaller.peek();
        }
    }
    private void rebalance() {
        if (this.smaller.size() > this.larger.size() + 1) {
            this.larger.add(this.smaller.poll());
        }
        else if (this.smaller.size() < this.larger.size()) {
            this.smaller.add(this.larger.poll());
        }
    }
}
```
{% endcode %}
