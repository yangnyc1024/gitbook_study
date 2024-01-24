# Question 3

直接用prefixSum一边计算，一边更新

```java
class Solution {
    public int maxSideLength(int[][] mat, int threshold) {
        int[][] prefixSum = new int[mat.length + 1][mat[0].length + 1];
        int result = 0;
        int sideLength = 1;
        for (int i = 1; i <= mat.length; i++) {
            for (int j = 1; j <= mat[0].length; j++) {
                prefixSum[i][j] = prefixSum[i-1][j] - prefixSum[i][j - 1] - prefixSum[i-1][j] + mat[i -1][j - 1];
                int curr = prefixSum[i][j] - prefixSum[i - sideLength][j] - prefixSum[i][j - sideLength] + prefixSum[i - sideLength][j - sideLength];
                if (i >= sideLength && j >= sideLength && curr <= threshold) {
                    result = sideLength;
                    sideLength++;
                }
            }
        }
        return result;
    }
}
```
