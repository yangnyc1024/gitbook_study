---
description: https://app.laicode.io/app/problem/125?plan=3
---

# Rotate Matrix

这种比较generate，从边上一直到中间，看看怎么rotate

<pre class="language-java"><code class="lang-java"><strong>public void rotate(int[][] matrix) {
</strong>    // assumptions: matrix is not null and has size of N * N, N >= 0
    int n = matrix.length;
    if (n &#x3C;= 1){
        return;
    }
    int round = n / 2;
    for (int level = 0; level &#x3C; round; level++) { // 对每个level进行处理
        int left = level;
        int right = n - 2 - level;
        for (int i = left; i &#x3C;= right; i++) { //对该层的每个点进行处理
            int temp = matrix[left][i];
            matrix[left][i] = matrix[n - 1 - i][left];
            matrix[n - 1 - i][left] = matrix[n - 1 - left][n - 1 - i];
            matrix[n - 1 - left][n - 1 - i] = matrix[i][n - 1 - left];
            matrix[i][n - 1 - left] = temp;
        }
    }
}
</code></pre>
