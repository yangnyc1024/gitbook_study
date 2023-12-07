# Problem 1: Longest Common Substring

substring问题讲究连续

### Method 1&#x20;

Step 1：DP定义

Step 2: Base Case

* dp\[0]\[0] = s\[i] = t\[j] ? 1:0

Step 3: Induction Rule

* dp\[i]\[j] =&#x20;
  * case 1: s\[i] == t\[j]
    * dp\[i]\[j] = dp\[i-1]\[j-1] + 1
  * case2: s\[i] != t\[j]
    * dp\[i]\[j] = 0
* recursion 角度？
  * s\[. i], t\[.  j] --->  s'\[, i -1), t'\[, j- 1)

Step 4: Fill in Order

* dp\[i-1]\[j- 1]
  * dp\[i]\[j]
* 从左到右，从上到下

Step 5: Return what

globalMax of all dp\[i]\[j]



```java
public String longestCommon(String source, String target) {
    char[] s = source.toCharArray();
    char[] t = source.toCharArray();
    
    int start = 0;
    int longest = 0;
    int[][] dp = new int[s.length][t.length];
    for (int i = 0; i < s.length; i++) {
        for (int j = 0; j < t.length; j++) {
            if (s[i] == t[j]) {
                if (i == 0  || j == 0) {
                    dp[i][j] = 1;
                } else {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }
            } 
           // else {
           //     dp[i][j] = 0;
           // }
           if (longest < dp[i][j]) {
               longest = dp[i][j];
               start = i - longest + 1; //记录开始点
           }
        
        }
        return source.substring(start, start + longest);
    }
}
```







### Method 2
