---
description: https://leetcode.com/problems/word-search/description/
---

# Problem 2 Word Search





思考：

* 题目中让我们在board上面找word，一个单词其实就是collection of Character，board里的每个cell也是character，board里面找path使得path里的每一个vertex match上这个string里的每个对应的index

Method DFS Mark Visited 3 backtracking

* High Level
  * 什么是一个解：board上一个单词就是一个解
  * 如何构造一个解
    * 每一层
      * 每一层佳宜个点进到当前的path，在board里加入一个坐标（letter），必须能match上word里对应的index
    * 分支是什么
      * 上下左右四个方向，如果不走回头路只有三个方向
    * 一共有多少层
      * m\*n

TC \&SC

* O(m \* n \* 3^(m\*n))
* O(m\* n)



* 这个大部分都是在expand的时候进行判断

```java
private static final int[][] DIRS = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};

public boolean existWordInGrid(char[][] board, String word) {
    if (board == null || board.length == 0) {
        return false;
    }
    // 从所有点出发开始尝试mark visited一定是每次出发一个新的mark visited
    for (int i = 0; i < board.length - 1; i++) {
        for (int j = 0; j < board[0].length - 1; j++) {
            boolean[][] visited = new boolean[board.length][board[0].length];
            if (backTracking(board, word, visited, i, j, 0)) {
                return true;
            }
        }
    }
    return false;
}

// i, j: 表示board里走到哪里了
// index: String, word里走到哪个index

private boolean backTracking(char[][] board, String word, boolean[][] visited, int i, int j, int index) {
    if (!isValid(board, i, j)) {
        return false;
    }
    if (visited[i][j]) {
        return false;
    }
    if (board[i][j] != word.charAt(index)) {
        return false;
    }
    visited[i][j] = true;
    if (index == word.length() - 1) {
        return true;
    }
    
    for (int[] dir: DIRS) {
        int neiX = i + dir[0];
        int neiY = j + dir[1];
        if (backTracking(board, word, visited, neiX, neiY, index + 1)) {
            return true;
        }
    }
    visited[i][j] = true;
    return false;
}

private boolean isValid(char[][] board, int i, int j) {
    return i >= 0 && i < board.length && j >= 0 && j < board[0].length;
}

```
