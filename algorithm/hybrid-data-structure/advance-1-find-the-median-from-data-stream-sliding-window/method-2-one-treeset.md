# Method 2 One TreeSet

not finished yet

````java
class Solution {
    private TreeSet<Element> window;
    private Element median;
    public double[] medianSlidingWindow(int[] nums, int k) {
        this.window = new TreeSet<>();
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
    private void add(int value ,int index) {
        Element ele = new Element(value, index);
        window.add(ele);
        if (median == null) {
            median = new Element(value, index);
        }
        // udpate median
        if (ele.compareTo(median) <= 0) {
            if (window.size() % 2 == 0) {
                median = window.floor(median);
            }
        }
        else {
            if (window.size() % 2 == 1) {
                median = window.ceiling(median); // 这个index 对么？
            }
        }
 
    }
    private void delete(int value, int index) {
        Element ele = new Element(value, index);
        window.remove(ele);
        // udpate median
        if (ele.compareTo(median) <= 0) {
            if (window.size() % 2 == 1) {
                median = window.ceiling(median);
            }
        }
        else {
            if (window.size() % 2 == 0) {
                median = window.floor(median); // 这个index 对么？
            }
        }
    }
    private double findMedian() {
        double result = 0.0;
        if (window.size() % 2 == 0) {
            result = (double) median.value /2.0 + window.ceiling(median).value /2.0;
        }
        else {
            result = (double) median.value;
        }
        return result;
    }

    class Element implements Comparable<Element> {
        int value;
        int index;
        public Element(int val, int idx) {
            this.value = val;
            this.index = idx;
        }
        @Override
        public int compareTo(Element that) {
            int result = Integer.compare(this.value, that.value);
            if (result == 0) {
                return Integer.compare(this.index, that.index);
            }
            return result;
        }
    }
}
```
````
