---
description: https://leetcode.com/problems/unique-paths-iii/description/
---

# Problem 3 Unique Path III



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
