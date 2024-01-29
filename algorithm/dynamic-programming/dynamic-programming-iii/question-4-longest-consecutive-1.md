# Question 4 Longest Consecutive 1

````java
```java
/*
step 1: dp definition
- dp[i] represent Longest Consecutive one length ending at i must including including including

step 2: base case
- dp[0] = nums[0]

step 3: induction rule
- dp[i] = nums[i] == 1? 1+ dp[i - 1]: 0 (你自己都不是1，ending at 你肯定没有全1subarray)

step 4: fill in order
- left to right

step 5: return what
- globalMax of all dp[i]

 */
class Solution {
    // public int findMaxConsecutiveOnes(int[] nums) {
    //     int[] dp = new int[nums.length];
    //     int max = nums[0];
    //     dp[0] = nums[0];
    //     for (int i = 1; i < nums.length; i++) {
    //         if (nums[i] == 1) {
    //             dp[i] = dp[i - 1] + 1;
    //             max = Math.max(dp[i], max);
    //         }
    //         else {
    //             dp[i] = 0;
    //         }
    //     }
    //     return max;
    // }
    public int findMaxConsecutiveOnes(int[] nums) {
        int[] dp = new int[nums.length];
        int max = nums[0];
        int curDP = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == 1) {
                curDP = curDP + 1;
                max = Math.max(curDP, max);
            }
            else {
                curDP = 0;
            }
        }
        return max;
    }
}
```
````
