# Problem 4: Longest Common Subsequence

Substring to Subsequece, subsequence不一定end with 该点



Step1 : DP定义

* dp\[i]\[j] represent Longest Common Subsequence S with length i, T with length j

Step 2: Base Case:

* dp\[0]\[any] = 0, dp\[any]\[0] = 0

Step 3: Induction Rule

* dp\[i]\[j] =&#x20;
  * s\[i- 1] == t\[j -1] ? dp\[i]\[j] = dp\[i - 1]\[j - 1] + 1
  * s\[i - 1]! = t\[j - 1] ? dp\[i]\[j] = max over(dp\[i-1]\[j], dp\[i]\[j-1],dp\[i-1]\[j-1])



{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```java
// Some code

public int longestCommonSubseq(String s, String t) {
    int[][] dp = new int[s.length() + 1][t.length() + 1];
    
    for (int i = 1; i <= s.length(); i++) {
        for (int j  = 1; j <= t.length(); j++) {
            if (s.charAt(i - 1) == t.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j- 1] + 1;
            } else {
                dp[i][j] = Math.max(dp[i -1][j], Math.max(dp[i][i - 1], dp[i - 1][j - 1]));
            }
        }
    
    }
    return dp[s.length()][t.length()];
}
```
{% endcode %}

空间上肯定可以优化，留行还是留列

