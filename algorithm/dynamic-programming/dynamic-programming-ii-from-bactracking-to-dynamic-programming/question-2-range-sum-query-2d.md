# Question 2 Range Sum Query 2D

#### Method 1 off by 1

Step1:DP定义

* prefixSum\[i]\[j] represent the sum from matrix\[0]\[0] to matrix\[i-1]\[j-1]<mark style="color:purple;">(这样做的以后，所有的人都有左边和上面)</mark>

Step 2: Base Case

* row 0 and col 0, off出来的行列：prefixSum

Step 3: induction rule

* prefixSum\[i]\[j] = <mark style="color:red;">matrix\[i-1]\[j-1]</mark> + prefixSum\[i]\[j-1] + prefixSum\[i-1]\[j] -prefixSum\[i-1]\[j-i]

Step 4:fill in order

* 左上到右下

Step 5: 时空间复杂度

* O(n^2)

Step 6: 如果你这么定义prefixSum,如何求Original Array里sum里(row1, col1)到(row2, col2)

* sum of original\[(row1, col1), (row2, col2)]&#x20;
* \=  prefixSum\[row2 + 1]\[col2+ 1] -  <mark style="color:orange;">prefixSum\[row1]\[col2+ 1]</mark>-  <mark style="color:orange;">prefixSum\[row2 + 1]\[col1] + prefixSum\[row1]\[col1]</mark>

```java
class NumMatrix {
    int[][] prefixSum;
    public NumMatrix(int[][] matrix) {
        this.prefixSum = new int[matrix.length + 1][matrix[0].length + 1];
    }


}
```

#### Method 2 NOT off by 1



javaStep1:DP定义

* prefixSum\[i]\[j] represent the sum from matrix\[0]\[0] to matrix\[i]\[j]\(ending at i, j, must including i, j)
* 原理完全不变，只不过，不是每个点都有上面和左面



```java

private void percalculation(int[][] matrix) {
    //单独讨论base case
    prefixSum[0][0] = matrix[0][0];
    for (int i = 1; i < matrix.length; i++) {
        prefixSum[i][0] = prefixSum[i-1][0] + matrix[i][0];
    }
    for (int j = 1; j < matrix[0].length; j++) {
        prefixSum[0][j] = prefixSum[0][j-1] + matrix[0][j];
    }
    for (int i = 1; i < matrix.length; i++) { //从上倒下
        for (int j = 1; j < matrix[0].length; j++) { // 从左到右
            prefixSum[i][j] = prefixSum[i-1][j]+  prefixSum[i][j-1] -prefixSum[i-1][j-1] + matrix[i-1][j-1];
        }
    }
}

public int sumRegion(int row1, int col1, int row2, int col2) {
    //单独讨论base case
    if (row1 == 0 && col1 == 0) {
        return prefixSum[row2][col2]'
    }
    if (row1 == 0) {   
        return prefixSum[row2][col2] - prefixSum[row2][col1 - 1];
    }
    if (col1 == 0) {   
        return prefixSum[row2][col2] - prefixSum[row1 - 1][col2];
    }
    return prefixSum[row2][col2] - prefixSum[row1 - 1][col2] - prefixSum[row2][col1 - 1] + prefixSum[row1 - 1][col1 - 1];
}
```
