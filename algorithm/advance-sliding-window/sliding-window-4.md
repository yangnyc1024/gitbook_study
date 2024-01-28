# Sliding Window 4

可以用的方法

* 2 pointer, k pointers
* 谁小移谁
* sliding window
  * fixed size sliding window
  * &#x20;shortest sliding window
  * longest sliding window

#### Q1 Given 3 sorted arrays, pick one element from each array to make a 3-tuple, find the number of 3-tuples where the difference <= target





#### Q1.1 Given 2 sorted array, pick one element from each array to make a pair, find number of pairs where the difference <= target







#### Q2 ALL DNA problem

Solution 1 Brute force



Solution 2 Fixed size sliding window + rolling hash

What is rolling hash？

* 新的hash = 4\* （旧的hash - 头部元素） + 尾部元素
* 用sliding window & bit operation



#### Q3.0 Word Distance I find the shortest distance of given 2 target words

Solution 1: brute force

Solution 2: 2 pointers？

* we only care about the most recent position

Solution 3:

* 先找出a,b两个element 的index，然后谁小移谁
* for each i :--> for this i, it is possible a or b
  * find the next closest j in the other array

Solution 3b:

* 两个指针，一个指向a，另一个指向b



#### Q3.1 Word Distance II , multi query

Solution 1: Use Q3.0

* each query takes O (n) guaranteed
* strategy: apply some precomputation to build a certain index to make the queries more efficient

Solution 2:&#x20;

option 1: if the number of distinct words is very small

* use full precomputation, 放进去Map\<Pair\<Char, Char>, min distance>

option 2: 如果N^2太大，只能做partial precomputation

* moderate/partial precomputation, 放进去Map\<String, List\<Integer>> invertIndex
* Inverted index的工业用途google search：
  * 输入key word，返回所有包含这个keyword的doc





#### Q3.2 Word Distance III k distinct words

Solution 1: Inverted index

* pick one lement from each of the k sorted arrays/lists, what is the minimum (max - min) value?
* 用sliding window II Q5.0里面的two pointers



Solution 2: Sliding window

* shortest sliding window满足：window中包含所有的string
* for each fast:
  * the min window ending at fast where it contains all the a,b,c
  * follow shortest sliding window 模版
* 需要支持的操作
  * 更新任意key对应的value
  * min(s.ValueSet())
* 用hashmap\<String, index> + treeMap\<index, string>
* 用double linkedlist
