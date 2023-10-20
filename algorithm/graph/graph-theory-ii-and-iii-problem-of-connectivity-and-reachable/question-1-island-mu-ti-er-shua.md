# Question 1 Island 母体二刷

### 解题步骤

#### Step 1: State the problem归大类

* Actually, this is a Graph Problem
* I want to model the problem to a Graph problem.

#### Step 2: Build Graph

* Let me build the graph.
* In my graph
  * my node/ vertex is every "1" cell in the matrix
  * edge: horizontally or vertically each one is connected with four directions with its neightbors

#### Step 3: 转化问题

* 脱马甲，这个问题其实本质上就是在解决你构建的哪个图上的什么问题
* 问一下面试官：OK, do you quite follow? Do you have any questions about the graph I built?
* So the problem is asking me to find out the number of islands, which is actually asking me how many <mark style="color:blue;">connected components</mark> are there in the graph I built

#### Step 4:这个问题在图论里面是个什么问题

* Therefore this is a traversal(reachable) problem in graph

#### Step 5: Propose 算法对比，选择最优

* DFS对点的遍历
* BFS对点的遍历
* 对比：时间空间复杂度，商讨具体实现的细节，选择一个最好的来写



### Method 1: DFS对点的遍历

```java
public Solution {
    // assumption: no duplicate edge
    private static final int[][] DIRS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    private static final char LAND = '1';
    private static final char WATER = '0';
    
    private int numberOfIsland(char[][] grid) {
       if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        int connectedComponent = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == LAND && !visited[i][j]) {
                    DFSMarkVisitedOne(grid, i, j,  visited);
                    connectedComponent++;
                }
            }
        }
        return connectedComponent;
    }
    private void DFSMarkVisitedOne(char[][] grid, int i , int j, boolean[][] visited) {
        if (visited[i][j]) return;
        visited[i][j] = true;
        for (int[] dir: DIRS) {
            int neiX = i + dir[0];
            int neiY = j + dir[1];
            if (!isValid(grid, neiX, neiY) || grid[i][j] == WATER) {
                continue;
            }
            DFSMarkVisitedOne(grid, neiX, neiY, visited);
        }
    }
    private boolean isValid(char[][] grid , int i, int j) {
        return i >= 0 && i < grid.length && j >= 0 && j < grid[0].length;
    }
}
```

思考：这样Mark Visited好么？

* boolean\[]\[] visited = new boolean\[grid.length]\[grid\[0].length];
* space: O(m\* n) for mark visited. + Call Stack: m\* n

其他的mark visited 的方式

* Set\<Integer> visited ==> X\* Col + Y ==> 含义 + overflow
* Set\<String> visited ==> X + "#" + Y
* Set\<Int\[]> visited ==> Set没法对数组去重
* Set\<List\<Integer>>visited ==> Set可以对List去重
* <mark style="color:blue;">好的写法：Set\<Node> visited;</mark>

&#x20;缺点1:

* boolean\[]\[] visited = new boolean\[grid.length]\[grid\[0].length];
* 不管我有没有走着点，都需要mark visited， 没有必要给这些0来开空间

缺点2:

* DFS is a method of Recursion: Call Stack还是很容易爆栈



### Method 2: BFS对点的遍历

Let me define in code what should a Node Object be looked like

如何让Set知道如何我们定义的两个Node Object是不是同一个Object？ Java Specific

**Override两个方法：**

* HashCode(unique hash value)
  * 用来知道这个item存在hashSet/Map里哪个柜子bucked(index)的
* Equals
  * 用来知道这个柜子里这么多东西有没有和你一样的

Map or Set

* What is the time to get or put or add?O(1)
* It looks like O(1) BUT in reality is that true? In Worst Case, it can be O(n) Collision

Rewrite HashCode

```java
class Node {
    int row;
    int col;
    public Node(int row, int col) {
        this.row = row;
        this.col = col;
    }
    @Override
    public int hashCode() {
        return this.row * 31 + this.col *31 * 31;
    }
    @Override
    public boolean equals(Object obj) {
        if (obj == this) {
            return true;
        }
        if (!obj instanceof Node) {
            return false;
        }
        Node temp = (Node) obj;
        return this.row == temp.row && this.col == temp.col;
    }
 }

```

Space: O(E)==> O(V)

```java
class Solution {
    int row;
    int col;
    public Node(int row, int col) {
        this.row = row;
        this.col = col;
    }
    @Override
    public int hashCode() {
        return this.row * 31 + this.col *31 * 31;
    }
    @Override
    public boolean equals(Object obj) {
        if (obj == this) {
            return true;
        }
        if (!obj instanceof Node) {
            return false;
        }
        Node temp = (Node) obj;
        return this.row == temp.row && this.col == temp.col;
    }
    private static final int[][] DIRS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    private static final char LAND = '1';
    private static final char WATER = '0';
    private int numberOfIsland(char[][] grid) {
       if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        int connectedComponent = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == LAND && !visited[i][j]) {
                    BFSMarkVisitedAtGeneration(grid, i, j,  visited);
                    connectedComponent++;
                }
            }
        }
        return connectedComponent;
    }
    private void BFSMarkVisitedAtGeneration(char[][] grid, int i, int j , Set<Node> visited) {
        Deque<Node> queue = new ArrayDeque<>();
        Node node = new Node(i, j);
        queue.offer(node);
        visited.add(node);
        while (!queue.isEmpty()) {
            Ndoe cur = queue.poll();
            for (int[] dir : DIRS) {
                int neiX = cur.row + dir[0];
                int neiY = cur.col. + dir[1];
                Node neighbor = new Node(neiX, neiY);
                if (isValid(grid, neiX, neiY) && grid[i][j] == LAND && !visited.contains(nei)) {
                    queue.offer(neighbor);
                    visited.add(neighbor);
                }
            }
        }
    
    
    }
    private boolean isValid(char[][] grid , int i, int j) {
        return i >= 0 && i < grid.length && j >= 0 && j < grid[0].length;
    }    

}
```

严格的 O(V+E), maximum O(V) space
