# Question 2 Russian Doll Envelopes

```java

/*
dp definition
- LIS[i] represent longest increasing subsequence ending at i must including i 

basic case
- LIS[0] = 1

induction rule
- LIS[i] = max(LIS[j] + 1) iff j < i && array[j] < array[i]
- array[j] < array[i] , which width[i] < width[j] && height[i] < height[j]

fill order
- from left to right

return what
- globalMax of all LIS[i]



 */

class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        if (envelopes == null || envelopes.length == 0) {
            return 0;
        }
        Arrays.sort(envelopes, (a, b) -> (Integer.compare(a[0], b[0])));

        int[] dp = new int[envelopes.length];
        Arrays.fill(dp, 1);

        int globalMax = 1;
        for (int i = 1; i < envelopes.length; i++) {
            for (int j = 0; j < i; j++) {
                if (compare(envelopes[i], envelopes[j])) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }

            }
            globalMax = Math.max(globalMax, dp[i]);
        }
        return globalMax;
    }
    private boolean compare(int[] array1, int[] array2) {
        return array1[0] > array2[0] && array1[1] > array2[1];
    }
}

```
