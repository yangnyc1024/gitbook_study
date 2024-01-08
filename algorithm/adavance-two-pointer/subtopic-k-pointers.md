# Subtopic: k pointers

&#x20;思路出发点，分解问题的方式并没有任何改变，start from brute force

* for all the tuples (i, j, k, l), where i in a, j in b, k in c, l in d;









## Question 3.0. Given two sorted arrays A and B, if there exist two numbers a from A and b from B, such that a+ b = target

1. 分解A\[i] + B\[j] ?= target
2. 移动方向？
   1. 当j往左边移动的时候
      1. B\[j]减少？
      2. A\[i] = target - B\[j]增大
      3. i往右移动

* 相向而行的双指针

3. implementation: we cannot miss any possibe j?



## Question 3.1 What about 3 sorted arrays? a+ b+ c = target from A, B, C



1. 分解 A\[i] + B\[j] + C\[k] = target
   1. 分解方式：固定k
2. for each K&#x20;



## Question 3.2 What about k sorted arrays?
