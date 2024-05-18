# Problem 2 Palindrome Partitioning II可以当母体练

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





````java
```java
/*
clarification:
assumption:
high level:
middle level:
TC &SC:
Cost: 30mins +30 mins + 30mins + 30mins
Comment:
    - 见dp讲章多种解法，一般dp，pure recursion，之前自己写的backTrakcing, 区间dp
    - 一个是在每个位置上，切或者不切的dp，空间小，但是时间长
    - 另一个是一刀一刀切，空间大，但是时间少了？不是 是把isPalindrome写成dp

- dp[i]  length i， how many cutting we need for it?
    - dp[i] = min (dp[j] + 1) for all j such that j < i if isPal(j + 1, i)
          = 0, iff isPal(0, i-1)


- dp[i][j]: represent  [i, j] (including i and j)if they are palindrome,
    base case
    induction rule:
        dp[i][j] = 
            if s.charAt(i) = s.charAt(j) dp[i][j] = dp[i+1][j- 1]
            if s.charAt(i) != s.charAt(j) dp[i][j] = false;
    filling:
        from buttom to up and from right to left
    return value
        dp[i][j]
    

*/
class Solution {
    public int minCut(String s) {
        // sanity check

        // intitial
        int[] dp = new int[s.length() + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        buildValidPali(s);
        dp[0] = 0;
        // System.out.println(Arrays.deepToString(isPali));
        // dp
        for (int i = 1; i <= s.length(); i++) {
            if (isPalindrome(s, 0, i-1)) { //!!!注意区别！！！！！！！
            // if (isPalindrome2(s, i-1, 0)) {
                // System.out.println(isPalindrome(s, 0 , i-1));
                // System.out.println(isPalindrome2(s, i-1, 0));
                dp[i] = 0;
            } else {
                for (int j = 0; j < i; j++) {
                    // if (dp[j] != Integer.MAX_VALUE && isPalindrome(s, j, i -1)) {
                    if (dp[j] != Integer.MAX_VALUE && isPalindrome2(s, i-1, j)) { ///
                        // System.out.println(isPalindrome(s, j , i-1));
                        // System.out.println(isPalindrome2(s, i-1, j));
                        dp[i] = Math.min(dp[i], dp[j] + 1);
                    }
                }
            }
        }
        // return value
        return dp[s.length()];
    }
    private boolean isPalindrome(String s, int i, int j) { // 注意有没有off by 1
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }   
        return true; 
    }
    private boolean[][] isPali;
    private void buildValidPali(String s) {
        isPali = new boolean[s.length()][s.length()];
        for (int i = s.length() - 1; i >= 0; i --) {
            for (int j = i; j < s.length(); j++) { //这个不是一个完整的matrix，因为没有j< i的情况
                if (i == j) {
                    isPali[i][j] = true;
                } else if (j == i + 1) {
                    isPali[i][j] = s.charAt(i) == s.charAt(j)? true: false;
                } else {
                    if (s.charAt(i)== s.charAt(j)) {
                        isPali[i][j] = isPali[i+ 1][j- 1];
                    }
                }
            }
        }
    }
    private boolean isPalindrome2(String s, int i, int j) {
        return isPali[j][i];
    }
}
```// Some code
````

