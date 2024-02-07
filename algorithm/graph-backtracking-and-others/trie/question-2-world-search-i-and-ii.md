# Question 2 World Search I& II

#### Method 1 DFS 3 all path

High level

* traverse all paths of the graph
* find a path that matches the target words

Middle Level

* each level:&#x20;
  * check current character if it matches the latter
  * if match, go next character
* level by level



```java
private static boolean helper(char[][] board, int x, int y, String word, int index, boolean[][] visited) {
    // basic case
    if (index == word.length()) {
        return true;
    }
    visited[x][y] = true;
    for (int[] dir: DIRS) {
        int neiX = dir[0] + x;
        int neiY = dir[1] + y;
        if (valid(neiX, neiY, board)) {
            if (helper(board, neiX, neiY, word, index + 1, visited)) {
                return true;
            }
        }
    }
    visited[x][y] = false;
    return false;
}
private boolean isValid(char[][] board, int x, int y) {
    return x >=0 && x< board.length && y >=0 && y < board[0].length;
}
```
