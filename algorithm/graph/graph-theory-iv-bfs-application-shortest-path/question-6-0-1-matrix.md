# Question 6 0-1 Matrix

### High Level

* it is a graph problem
  * vertex: matrix里的每个点
  * edge: four direction
* 所以这道题在我们构建的图里面：对于每一个点，都填好离他最近0的距离
* 本质上是一个最短路径问题， all to any的问题

#### Method KBFS

* instead of从每一个1出发，做一遍S1(O \* (V \* (V+E)))
* 从所有的0一起出发，只要遇到一个1，这个1的最短路径就确定了
  * 从any 0 cell to this 1 = from this 1 to any 0

**Question：从所有的(all)1一起出发，一起放进queue可以吗？**

* 我让你求的是每一个1到最近0的距离，你从任意一个1一起出发，假设你到了一个0以后，是哪个1到呢？就算一个到了，别的1也没到啊，没法填结果



```java
// Some code



public int[][] updateMatrix(int[][] matrix) {
    // assume matrix is valid
    Deque<Point> queue = new ArrayDeque<>();
    Set<Point> visited = new HashSet<>();
    
    // KBFS Generate all possible starting source node
    for (int i = 0; i < matrix.length; i++) {
        for(int j = 0; j < matrix[0].length; j++) {
            if (matrix[i][j] == 0) {
                Point new Point = new Point(i, j);
                queue.offer(newPoint);
                visited.add(newPoint);
            }
        
        }
    }
    int level = 0;
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            Point cur = queue.poll();
            matrix[cur.x][cur.y] = level;
            for (int[] dir: DIRS) {
                int neiX = cur.x + dir[0];
                int neiY = cur.y + dir[1];
                if (isValid(matrix, neiX, neiY) && visited.add(nei)) {
                    queue.offer(nei);
                }
            }
        }
        level++;
    }
    return matrix;
}
```

