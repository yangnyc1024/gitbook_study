# Question 3 Seven Puzzle

## 理解题目

* 一个board，每次吧这个borad里的某一个数字和其他人do something
* 一个单词，每次把这个单词里的某一个char do something
* 套路：以整体结构作为点，做隐式图搜索



## High Level

* this is a graph problem
  * vertex：整体的board是一个点
  * edge：通过一次操作（把0和四个方向交换）能到的点都是neighbor，
* this is a  actually S1 in Shortest Path Problem



### Method BFS

```java
// Some code

private static final int[][] DIRS = {{1,0}, {-1, 0}, {0,1}, {0, -1}};
class Board {
    private static final int R= 2;
    private static final int C = 3;
    private int[][] board = new int[R][C];
    private int[] indexOfZero = new int[2];
    public Board(int[][] target) {
        for (int = 0; i < target.length; i++) {
            for (int j = 0; j < target[0].length; j++) {
                if (target[i][j] == 0) {
                    this.indexOfZero[0] = i;
                    this.indexOfZero[1] = j;
                }
                this.board[i][j] = target[i][j];
            }
        }
    }
    public Board(Board original) {
        int[][] target = original.board;
         for (int = 0; i < target.length; i++) {
            for (int j = 0; j < target[0].length; j++) {
                if (target[i][j] == 0) {
                    this.indexOfZero[0] = i;
                    this.indexOfZero[1] = j;
                }
                this.board[i][j] = target[i][j];
            }
        }
    }
    @Override
    public int hashCode() {
        int code = 0;
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                code = code * 31 + this.board[i][j];
            }
        }
    }
    @Override
    public boolean equals(Object obj) {
        if (obj == this) return true;
        if (!obj instanceof Board) return false;
        // if (obj != null && obj.getClass() != this.getClass()) return false;
        Board temp = (Board) obj;
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (temp.board[i][j] != this.board[i][j]) {
                    return false;
                }
            }
        }
        return true;
    }  
}
private boolean isValid(Board board, int i ,int j) {
    return i >= 0 && j >= 0 && i < board.R && j < board.C;
}
// 我想把这个board里面的0和你给我一个方向进行交换

private void swap(Board board, int[] dir) {
    int[] indexOfZero = board.indexOfZero;
    int[] newIndex = new int[]{indexOfZero[0] + dir[0], indexOfZero[1] + dir[1]};
    board.board[indexOfZero[0]][indexOfZero[1]] = board.board[indexOfZero[0] + dir[0]][indexOfZero[1] + dir[1]];
    board.board[indexOfZero[0] + dir[0]][indexOfZero[1] + dir[1]] = 0;
    board.indexOfZero = newIndex;
}

```
