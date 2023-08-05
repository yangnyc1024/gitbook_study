---
description: https://leetcode.com/problems/sliding-window-median/
---

# Find the Median from Data Stream/Sliding Window

## Question

You are given an integer array `nums` and an integer $$k$$. There is a sliding window of size $$k$$ which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the median array for each window in the original array_. Answers within $$10^{-5}$$ of the actual value will be accepted.

## Hint

* <mark style="color:blue;">What is the median?</mark>&#x20;
  * it is the middle point in a dataset
  * it is half of the data points are smaller than the median, and half of the data points are larger.&#x20;
  * max(smaller part) + min(larger part)
* find two data structures and maintain they balance
* Also, this concept can extend to 25th quantile, or whatever ?? quantile

## Solution

#### High Level

* find two data structures to store all the elements, and make sure these two data structures satisfy the following two properties
  * <mark style="color:blue;">**value wise**</mark><mark style="color:blue;">:</mark> max(the smaller half)  < min(the larger half)
  * <mark style="color:blue;">**size wise**</mark><mark style="color:blue;">:</mark>&#x20;
    * when #element = old, smaller.size > larger.size + 1
    * when #element = even, smaller.size = larger.size
* By keeping these two data structures balanced, we can ensure that the median is either the maximum element of the max-heap or the minimum element of the min-heap.

#### Middle Level

* We would like to help some APIs
  * insert(int <mark style="color:orange;">num</mark>)
  * delete(int num)
  * findMedian()
* for insert/ delete
  * 1\) as we know the maximum(smaller half), and minimum(larger half), compare this <mark style="color:orange;">num</mark> with these two
    * <mark style="color:orange;">maximum(smaller half) \&minimum(larger half)</mark>
    * to choose which half you would like to put this num in
  * 2\) maintain <mark style="color:orange;">the size property</mark>
* <mark style="color:orange;">find median</mark>
  * \#element == even?&#x20;
    * (maximum(smaller half) + minimum(larger half) ) / 2
  * \#element == old
    * maximum(smaller half)&#x20;



[method-1-two-heap.md](method-1-two-heap.md "mention")

* insert(int <mark style="color:orange;">num</mark>) ---> $$O( \log n)$$&#x20;
* delete(int num)---> $$O(n)$$
* findMedian() --->$$O(1)$$&#x20;

[method-2-not-recommend-two-treemaps-one-treemap.md](method-2-not-recommend-two-treemaps-one-treemap.md "mention")

* insert(int <mark style="color:orange;">num</mark>) ---> $$O( \log n)$$&#x20;
* delete(int num)---> $$O(\log n)$$
* findMedian() --->$$O(1)$$&#x20;
