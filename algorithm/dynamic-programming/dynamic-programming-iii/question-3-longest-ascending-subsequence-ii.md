# Question 3 Longest Ascending Subsequence II

这个需要还原，还原的本质，就是知道每一步从哪里来？

* 你再记录一个呗。。。。pre\[]



```java
/*
dp defefinition:
- dp[i] represent LIS ending at i must including i
- prev[i] represent the former element in the longest increasing subsequence ending at i

base case
- dp[0] = 1
- prev[0] = -1

induction rule
- dp[i] = Math(dp[j] + 1) iff j < i , array[j] < array[i]
- prev[i] = j iff j < i , array[j] < array[i]

fill in order
- left to right

return what
- start from the prev[end], which end is the end of the longest index, 
- put int[prev[i]] as result, and the length = dp[array.length]
*/

public class Solution {
  public int[] longest(int[] a) {
    // Write your solution here
    // sanity check
    if (a == null || a.length == 0) {
      return null;
    }

    // intial prev& dp
    int[] dp = new int[a.length];
    int[] prev = new int[a.length];

    // base case
    Arrays.fill(prev, -1);
    Arrays.fill(dp, 1);
    int globalMax = 1;
    int longestEndingIndex = 0;

    // induction rule
    for (int i = 1; i < a.length; i++) {
      for (int j = 0; j < i; j++) {
        if (a[i] > a[j]) {
          if (dp[i] < dp[j] + 1) { //   dp[i] = Math.max(dp[i], dp[j] + 1);
            dp[i] = dp[j] + 1;
            prev[i] = j;
          }
        }
      }
      // 相当于检查下每次你更新后，是否有新的
      if (dp[i] > globalMax) {
        globalMax = dp[i];
        longestEndingIndex = i;
      }
    }


    // post processing
    int[] result = new int[globalMax];
    for (int i = longestEndingIndex; i >= 0; i = prev[i]) {
        result[globalMax - 1] = a[i];
        globalMax--;
    }
    return result;
  }
}

```
