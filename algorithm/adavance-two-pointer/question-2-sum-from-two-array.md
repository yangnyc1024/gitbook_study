---
description: Question
---

# Question 2\* Sum from two array

Given two arbitrary arrays(with possible duplicate), pick one element from each of the array, find all pairs with the largest sum <= target.

#### Solution 1: binary search

TC: O(mlogm + nlogn + n logm), assume n is smaller

#### Solution 2: 相向而行的two pointer

step1 确定能用2pointer，相向

step2 initialzation of i，j position

&#x20;TC: O(nlogn + mlogm + m+ n)



#### Solution 3 treeMap
