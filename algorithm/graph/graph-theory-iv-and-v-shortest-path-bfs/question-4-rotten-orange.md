# Question 7 Rotten Orange

```java
// Some code




public int originalRotting(int[][] matrix) {
    // assume matrix is valid
    Deque<int[]> queue = new ArrayDeque<>();
    int count = 0;
    
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix[0].length; j++) {
            if (matrix[i][j] == ROTTEN_ORANGE) {
                queue.offer(new int[] {i, j});
            } 
            else if (matrix[i][j] == FRESH_ORANGE) {
                count++;
            }
        }
    }
    int real = 0; // 世纪腐蚀了多少个橘子
    int level = 0;
    while (!queue.isEmpty()) {
        
    
    }
}
```
