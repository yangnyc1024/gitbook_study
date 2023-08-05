---
description: Powered by ChatGPT-4
---

# Tool: Quick Select

#### Summary

<mark style="color:blue;">**Quickselect**</mark> is an algorithm

* find the kth smallest (or largest) element in an unordered list
* related to the quicksort sorting algorithm

#### **High Level**

* works by using a "<mark style="color:blue;">divide and conquer</mark>" strategy&#x20;
* to <mark style="color:blue;">efficiently narrow down</mark> the possible <mark style="color:red;">locations</mark> of the desired element.

#### Mid Level

Step 1:&#x20;

* By <mark style="color:red;">choosing a "pivot" element</mark> from the array
* By [<mark style="color:red;">partitioning</mark>](#user-content-fn-1)[^1] the other elements into two sub-arrays
  * <mark style="color:orange;">according to</mark> whether they are less than or greater than the pivot value

Step 2:&#x20;

* By comparing the <mark style="color:red;">pivot final index and index k</mark>, the algorithm recurses into the part where the kth index element is&#x20;
* until the pivot final index == k, we finally get the result

This means the algorithm doesn't have to sort all the elements. As a result, it is more efficient in finding the kth smallest (or largest) element than sorting the whole array.

#### **Detailed Explanation**

Now, let's dive into a detailed explanation. Suppose we're looking for the kth smallest element in the list.

1. **Select a pivot**: The pivot selection can be random, but it often helps if the pivot is near the median of the list. There are different strategies to select a pivot, but for simplicity, you can just pick the first or the last element in the array.
2. **Partition the array**: Reorder the array so that all elements with values less than the pivot come before the pivot, while all elements with values greater than the pivot come after it (equal values can go either way). After this partitioning, the pivot is in its final position. This is called the partition operation.
3. **Recursion**: If the pivot index is k, we found the kth element, so we return it. If k is less than the pivot index, the kth smallest must be in the left part of the array, so we recursively apply the quickselect to the left part. If k is greater than the pivot index, it must be in the right part, so we recursively apply quickselect to the right part.

The key insight is that, just like quicksort, every time we perform a partition operation, we are guaranteed that the pivot element is in its rightful place (i.e., all elements to its left are smaller, and all elements to its right are larger). The main difference between quicksort and quickselect is that while quicksort recurses on both sides of the partition, quickselect only recurses on one side.

#### **Time Complexity**

The average-case time complexity of Quickselect is $$O(n)$$, which is quite efficient. However, the worst-case scenario is $$O(n^2)$$, when the selected pivot is the smallest or the largest element in the array. This case leads to the array being partitioned into two parts of size 0 and n-1, like in the worst-case scenario of quicksort. These bad cases can be avoided with a good pivot selection strategy.



#### Code(Java)

[https://leetcode.com/problems/kth-largest-element-in-an-array/](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
class Solution {
    int[] nums;
    public int findKthLargest(int[] nums, int k) {
        this.nums = nums;
        int length = this.nums.length;
        return quickselect(0, length - 1, length - k); // you would like to have kth largest, i.e.  length - k index
    }
    private int quickselect(int left, int right, int k_index) {
        // return the value of 
        if (left == right) {
            return this.nums[left];
        }
        Random random = new Random();
        int initial_pivot_idx = left + random.nextInt(right - left);
        int final_pivot_idx = partition(left, right, initial_pivot_idx);
        if (final_pivot_idx < k_index)  {
            return quickselect(final_pivot_idx + 1, right, k_index);  // pivot is correct, dont need to go into the recurrcence
        }
        else if (final_pivot_idx > k_index) {
            return quickselect(left, final_pivot_idx - 1, k_index);
        }
        else {
            return this.nums[k_index];
        }
    }
    private int partition(int left, int right, int initial_pivot_idx) {
        int curPivotValue = this.nums[initial_pivot_idx];
        swap(right, initial_pivot_idx);
        int sortedIndex = left;
        for (int i = left; i <= right; i++) {
            if (this.nums[i] < curPivotValue) {
                swap(i, sortedIndex);
                sortedIndex++;
            }
        }
        swap(sortedIndex, right); // this would the first index which is >= curPivotValue
        return sortedIndex;
    }
    private void swap(int left, int right) {
        int temp = this.nums[left];
        this.nums[left] = this.nums[right];
        this.nums[right] = temp;
    }
}
```

[^1]: 
