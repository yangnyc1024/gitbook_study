# Problem 3: Edit Distance母体



&#x20;Pure Recursion怎么做？

Step 0: Function定义

* int  editDistance(String word1, String word1Length, String word2, String word2Length):
  * 给我一个长度为word1Length 的word 1和一个长度为word2Length的word 2， 我能返回，最少需要几次操作就能把word1通过replace, delete, insert 三种操作变成word 2

Step 2 ： base case

* word1Length = 0, return word2Length
* word2Length = 0, return word1Length

Step 3: subproblem

* editDistance(word1, word1Length - 1, word2, word2Length - 1)（replace or do nothing）
* editDistance(word1, word1Length, word2, word2Length - 1) （insert）
* editDistance(word1, word1Length - 1, word2, word2Length) （deleted）

Step 4: Recursion rule
