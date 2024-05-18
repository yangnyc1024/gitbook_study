# Problem 4 Valid Palindrome III



````java
```java
/*
Clarification:
    - check if you need to remove how many character to make it is a isValidPalindrome
Assumption:
    - valid?
High Level
    - Method 1: check the inverse string , if we can find the maximum 
        ==> longest common subsequence
        ==> 什么情况下， 我就没有办法通过至多k次操作变成回文？不common的部分多于k个
    - Method 2: check the interval between i, j , how many move we need for
Middle Level
Method 1.0:
    - dp mean? dp[i][j] represents longest common sequence, 
        ends with the first seq ith, including ith index
        ends with the second seq jth, including jth index
    - basic case: dp[0][0] = 0;
    - induction rule:
        - dp[i][j] = max(dp[i-1][j-1] + 1, dp[i-1][j], dp[i][j-1]), if s.charAt(i -1) = sRev.charAt(j-1),
        - dp[i][j] = max(dp[i-1][j-1] , dp[i-1][j], dp[i][j-1]), if s.charAt(i-1)!= sRev.charAt(j-1)
    - filling 
        - from up to down, from left to right
    - return result
        - dp[s.length][s.length]  >= s.length()-k?
Method 1.1:
    - preDial =? 
    - top = dp[i] //这相当于上一行的头顶那个element
    - if text1.charAt(i) == text2.charAt(j), dp[i] = max(dp[i-1], preDial + 1, top);
    - else: dp[i] = max(dp[i-1], preDial, top)
    - preDial = top, top = dp[i] //preDial往右移动一格，top也往右移动一格
Method 2:
    - dp means? dp[i][j] represents the minimum remove elements
    - base case
    - induction rule: i < j
        dp[i][j] = 
            j - i == 0? dp[i][j] = 0
            j - i == 1?  dp[i][j] = s.charAt(i) ==s.charAt(j) ? 0: 1;
            j - i == others
                dp[i][j] = s.charAt(i) == s.charAt(j) ? 
                    Math.min(dp[i+1][j-1], Math.min(dp[i+1][j] + 1, dp[i][j-1] + 1)) : Math.min(dp[i+1][j-1] + 2, Math.min(dp[i][j-1] +1, dp[i+1][j] + 1));
                    // dp[i+1][j-1] : Math.min(dp[i][j-1] + 1, dp[i+1][j] + 1);
    - filling order
        - from bottom to top
        - from left to right?
        - (0,0) (0,1) (1,1)
        -        (1,1), (1,2)
        -               (2,2)
        - filling (2,2), (1,1), (1,2),....
    - return dp(0, s.size - 1) < k?
    - TC(n^2), SC(n^2)

Comment: 
    - method 1: 你reverse以后，如果不match说明要换，，所以要找的是最长的common sequence,not a 
    - method 2: 
Cost: 45mins + 15mins + 60mins + 30mins

*/


class Solution {
    public boolean isValidPalindrome(String s, int k) {
        // sanity check

        // initial 
        int size = s.length();
        int[][] dp = new int[size][size];

        // dp and filling
        for (int i = size - 1; i >= 0; i--) {
            for (int j = i; j < size; j++) {
                if (j - i == 0) {
                    dp[i][j] = 0;
                }
                else if (j - i == 1){
                    dp[i][j] = s.charAt(i) ==s.charAt(j) ? 0: 1;
                } else {
                    dp[i][j] = Integer.MAX_VALUE;
                    dp[i][j] = s.charAt(i) ==s.charAt(j) ? 
                        Math.min(dp[i+1][j-1], Math.min(dp[i+1][j] + 1, dp[i][j-1] + 1)) : Math.min(dp[i+1][j-1] + 2, Math.min(dp[i][j-1] +1, dp[i+1][j] + 1));
                        // dp[i+1][j-1] : Math.min(dp[i][j-1] + 1, dp[i+1][j] + 1);
                }
            }
        }

        // return value
        return dp[0][size -1] <= k? true: false;
    }
}
```
````
