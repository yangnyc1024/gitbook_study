# Problem 2 Largest Sum of Averages







Step 3: Induction Rule

* dp\[k]\[i] = 假设考虑切点切在了左大段长度为j
* Max (dp\[k - 1]\[j]  + sum\[j...i] /i-j+1)&#x20;
* Max(左大段 + 右小段)

左大段的长度j是任意的么？

* 左大段要继续把j长度的item分割为k-1份，左大段的长度最少也得有k-1这么长



Step 4: fill in order

* dp\[k - 1]\[j] , dp\[k]\[i]
* 从上到下，从左到右



```java
public double largestSumAverage(int[] array, int k) {
    // assume array is valid
    double[][] dp = new double[k+1][array.length + 1];
    double[] prefixSum = new double[array.length + 1];
    
    for (int i; i <= array.length; i++) {
        prefixSum[i] = prefixSum[i - 1] + array[i - 1];
    }
    // base case
    for (int i = 1; i <= array.length; i++) {
        dp[1][j] = prefixSum[i]/i;
    }
    
    // 把长度为j东西，分成i份：dp[i][j]
    for (int i = 2; i <= k; i++) {
        for (int j = i; j <= array.length; j++) { // 长度
            if (i = j) {
                dp[i][j] = dp[i - 1][j - 1] + array[j- 1]/ 1;
            }
            else {
                for (int leftLength = i - 1; leftLength < j; leftLength++) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][leftLength] + (prefixSum[j] - prefixSum[leftLength]) / (j - leftLength));
                }
            }
        }
    }
    return dp[k][array.length];
}
```

TC: O(NK\*N) ==> O(N^2 \*K)

SC: KN-> N





### Method 2:&#x20;

* 其实存一行就行了dp\[k]\[n] only depends on dp\[k-1]\[n2]存一行就可以

Induction Rule

* dp\[k - 1]\[n2] --- dp\[k]\[n]
* 假如现在只有一行
  * \[last row n2 <- current row n]
  * 更新顺序要改变
* from right to left:你左边的值都是还没有更新过的值







