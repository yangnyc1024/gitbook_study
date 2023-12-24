# Problem 2 Palindrome Partitioning III可以当母体练

区间型DP + NK问题

NK问题: divide s into k nonempty disjoint substrings

* dp\[k]\[n] represents the minimum number of characters you need to change to divide the length n string into k parts
* dp\[1]\[n] = 这一段需要change多少个就是多少
* dp\[k]\[i] = min (dp\[k-  1]\[j] + 右小段需要change多少个就是多少个）

逻辑: 先知道给你一段，最少需要change几个把它变成回文

* numberOfChange\[i]\[j] represents from i to j, the minimum number of characters you need to change to make i to j a palindrome
* numberOfChange\[i]\[i] = 0
* numberOfChange\[i]\[i+1] = s\[i] != s\[j]? 1: 0
* numberOfChange\[i]\[j] =&#x20;
  * s\[i] = s\[j]: numberOfChange\[i]\[j] = numberOfChange\[i+ 1]\[j - 1]
  * s\[i] != s\[j]: 1 + numberOfChange\[i + 1]\[j - 1]
