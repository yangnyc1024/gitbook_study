---
description: https://leetcode.com/problems/unique-paths-iii/description/
---

# Problem 3 Unique Path III

#### 思考

注意对比经典模型：二方向，左上道右下，有多少总方法到达：dynamic programming模型

Step 1：

* 这是个graph的问题
* vertex： matrix里的每一个坐标，edge：上下左右四个方向

Step 2：道出本质

* 人家问我们一共有多少种走出所有空地从start道end
* 从start到end所有可能的走过所有空地的路径数量



#### Method Backtracking(dfs mark visited3)

**High Level**

* 每一层：走一步
* 分支：下一步往哪里走，不出界不是障碍物
* 一共多少层：空地层

**Detail Logic**

* walk over every non-obstacle square exactly once != walk over every empty square exactly once
  * 1 representing the starting square. There is exactly one starting square
  * 2 representing the ending square. There is exactly one ending square
  * 0 representing empty squares we can walk over
  * \-1 representing obstacle that we cannot walk over

1. 没给start and end 怎么办？只能遍历
2.  你怎么知道你走没有走完所有non -obstacles cell呢？

    必须要保证世纪走过的空地数 = 总的空地数

#### TC & SC

* TC : O(3^m\*n)
* SC: O(m\* n)







```java
private static final int START = 1;
private static final int END = 2;
private static final int EMPTY = 0;
private static final int OBSTACLE = -1;
private static final int[][] DIRS = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};

public int numberOfUniquePath(int[][] grid) {
    // assume grid valid
    int startX = 0;
    int startY = 0;
    
    int countNon = 0;
    // step 1: searching for start and end, count how many empty space
    for (int i = 0; i < grid.length; i++) {
        for(int j = 0; j < grid[0].length; j++) {
            if (grid[i][j] != OBSTACLE) {
                countNon++;
            }
            if (grid[i][j] == START) {
                startX = i;
                startY = j;
            }
        }
    }
    boolean[][] visited = new boolean[grid.length][grid[0].length];
    int[] result = new int[]{0};
    dfs(startX, startY, visited, grid, countNon, result, 1);
    return result[0];
}


private void dfs(int i, int j, boolean[][] visited, int[][] grid, int countNon, int[] result, int count) {
    if (visited[i][j]) {
        return;
    }
    if (grid[i][j] == END && countNon == count) {
        result[0] ++;
        return;
    }
    visited[i][j] = true;
    for (int[] dir: DIRS) {
        int neiX = i + dir[0];
        int neiY = j + dir[1];
        if (isValid(grid, neiX, neiY)) {
            dfs(neiX, neiY, visited, grid,countNon, result, count + 1);
        }
    }
    visited[i][j] = false;
}
private boolean isValid(int[][] board, int i, int j) {
    return i >= 0 && i < board.length && j >= 0 && j < board[0].length;
}
```
