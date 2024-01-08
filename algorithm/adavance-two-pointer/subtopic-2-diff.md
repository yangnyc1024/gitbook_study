# Subtopic: 2-diff

## Question 0 : 2sum, given a sorted array, determines if there isa pair of elements sum to target





## Question 1: 2 -dff, how many pairs diff = target(\<target, >target), where target > 0?

### Question 1.1: How many pairs with diff = x- y = target in a sorted array without duplicates?



assumption?

* assending?
* no duplicate?
* target is positive?
* different =| y - x|
* <1,4>, <4,1>是不是同一个pair

#### Solution 1: Brute Force





#### Solution 2: 2-pointer

* option 1: linear search
* option 2: binary search using sorted array， O(logn )
* option 3: hashset/hashmap record all the lemetns before j
* option 4: 同向而行的two pointers

<figure><img src="../.gitbook/assets/Screenshot 2024-01-07 at 1.28.34 PM.png" alt="" width="375"><figcaption></figcaption></figure>

### Q1.2  A little Advance Version: how many pairs with diff > target







### Q1.3 The array is unsorted , different is |x-y|









## Q2 Given a sorted integer array, find unumber of subsets satisfying the property of <mark style="color:red;">max(subset) - min (subset)</mark> <= target

Clarification:

* target> 0
* no duplicates in the sorted array
* subset size >= 1

Solution 1 Brute Force

* for all subset: if (max - min < = target): count++;

