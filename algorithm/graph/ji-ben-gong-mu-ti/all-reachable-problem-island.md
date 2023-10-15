---
description: https://leetcode.com/problems/number-of-islands
---

# All reachable problem ---island

Island problem, 可以是一张图上，1）flood fill, 2) number of islands, 3) max area of the island

## Question

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Clarification & Assumption

* Graph Representation
  * vertex: 所有是<mark style="color:blue;">“1”</mark> 的点
  * edge: four directions 为 <mark style="color:blue;">“1”</mark> 的点

### High Level

* Problem definition
  * this is an all-reachable nodes problem
  * starting from <mark style="color:blue;">every 1</mark> vertex, traversing all connected element
* What traversal algorithm?
  * DFS1, DFS2, DFS3(for each vertex, traverse all possible reachable vertex, by depth order, and make sure each vertex visited once)
  * BFS(for each vertex, traverse all possible reachable vertex, by level/breath order, and make sure each vertex visited once)

### Middle Level

* Graph representation?&#x20;
  * Method 1: 完全分开
    * graph representation
      * vertex, int\[]\[]
      * edge: four direction {-1, 0} {1, 0}, {0, -1}, {0, 1}
    * visited: boolean visited\[]\[]
  * Method 2: 把visited单独出来
    * graph representation
      * Vertex: cell (int x, int y)
      * edge: four direction {-1, 0} {1, 0}, {0, -1}, {0, 1}:&#x20;
    * visited: enum / boolean visited\[]\[]
  * Method 3: 全部合在一起
    * Graph Representation, vertex & edge together
      * Vertex& Edge
      * Graph
        * Node {int x, int y, int value, boolean visited, Set\<Vertex> neighb}

#### TC & SC

* TC: O(|V| + |E|) = O (5mn), SC: O(mn)





#### Method 1 DFS

```java
class Solution {
    private static final int[][] DIRS = new int[][] {{-1, 0}, {0, -1}, {1, 0}, {0, 1}};
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        int count = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (visited[i][j] == false && grid[i][j] == '1') {
                    dfs(grid, i, j, visited);
                    count++;
                }
            }
        }
        return count;
    }
    private void dfs(char[][] grid, int row, int col, boolean[][] visited) {
        // // check visited
        if (!isValid(grid, row, col) || visited[row][col] || grid[row][col] != '1') {
            return;
        }
        // mark visited
        visited[row][col] = true;

        // visiting neighbor
        for (int[] dir : DIRS) {
            int neiX = row + dir[0];
            int neiY = col + dir[1];
                dfs(grid, neiX, neiY, visited);
        }
 
    }
    private boolean isValid(char[][] grid, int row, int col) {
        return row >= 0 && row < grid.length && col >= 0 && col < grid[0].length;
    }
}
```

#### Method 1 BFS (& DFS)

```java
class Solution {
    class Cell {
        int x;
        int y;
        public Cell (int x, int y) {
            this.x = x;
            this.y = y;
        }
        public int hashCode() {
            return this.x * 31 + this.y;
        }
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null) return false;
            if (this.getClass() != obj.getClass()) {
                return false;
            }
            Cell that = (Cell)obj;
            return this.x == that.x && this.y == that.y;
        }
    }
    public int numIslands(char[][] grid) {

        //sanity check
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }

        // build graph

        // build visited check
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        // bfs && dfs
            // initial
            // expand & generate
        int[] count = new int[1];
        for (int x = 0; x < grid.length; x++) {
            for (int y = 0; y < grid[0].length; y++) {
                if (grid[x][y] == '1' && visited[x][y] == false) {
                    Cell root = new Cell(x, y);
                    // bfs(grid, visited, root);
                    dfs(grid, visited, root);
                    count[0]++;
                }
            }
        }
        return count[0];
    }
    private void dfs (char[][] grid, boolean[][] visited, Cell root) {
        if (!isValid(root.x, root.y, grid) || visited[root.x][root.y] || grid[root.x][root.y] != '1') {
            return;
        }
        visited[root.x][root.y] = true;
        for (int[] dir : DIRT) {
            int neiX = root.x + dir[0];
            int neiY = root.y + dir[1];
            Cell nei  = new Cell(neiX, neiY);
            dfs(grid, visited, nei);
        }
    }   
    private void bfs (char[][] grid, boolean[][] visited, Cell root) {        
        Queue<Cell> queue = new ArrayDeque<>();
        queue.offer(root);
        visited[root.x][root.y] = true;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Cell cur = queue.poll();
                for (int[] dir: DIRT) {
                    int neiX = cur.x + dir[0];
                    int neiY = cur.y + dir[1];
                    Cell nei = new Cell(neiX, neiY);
                    if (isValid(neiX, neiY, grid) && grid[neiX][neiY] == '1' && visited[neiX][neiY] == false) {
                        queue.offer(nei);
                        visited[nei.x][nei.y] = true;
                    }
                }

            }
        }  
    }
    private boolean isValid (int x, int y, char[][] grid) {
        return  x >= 0 && x < grid.length && y >=0 && y < grid[0].length;
    }
    private static final int[][] DIRT = new int[][] {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
}
```

#### Method 3 BFS & DFS

```java
class Solution {
    class Vertex {
        int x;
        int y;
        Set<Vertex> neighbors;
        boolean visited;
        char value;
        public Vertex(int x, int y, char value) {
            this.x = x;
            this.y = y;
            this.neighbors = new HashSet<>();
            this.visited = false;
            this.value = value;
        }
        @Override
        public int hashCode() {
            return this.x * 31 + this.y;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null) return false;
            if (this.getClass() != obj.getClass()) {
                return false;
            }
            Vertex that = (Vertex) obj;
            return this.x == that.x && this.y == that.y;
        }
    }
    public int numIslands(char[][] grid) {
        // sanity check

        // buildGraph
        Set<Vertex> graph = buildGraph(grid);

        // traverse
        int count = 0;
        for (Vertex root: graph) {
            if (isValid(root.x, root.y, grid) && root.value == '1' && root.visited != true) {
                // bfs(root, graph, grid);
                dfs(root, graph, grid);
                count++;
            }
        }
        return count;
    }
    private void bfs(Vertex root, Set<Vertex> graph, char[][] grid) {
        Queue<Vertex> queue = new ArrayDeque<>();
        queue.offer(root);
        root.visited = true;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Vertex cur = queue.poll();
                for (Vertex nei: cur.neighbors) {
                    if (isValid(nei.x, nei.y, grid) && nei.visited != true && nei.value == '1') {
                        queue.offer(nei);
                        nei.visited = true;
                    }
                }
            }
        }
    }
    private void dfs(Vertex root, Set<Vertex> graph, char[][] grid) {
        // base case
        if (root.visited == true) {
            return;
        }

        // cur step visited?
        root.visited = true;

        for (Vertex nei: root.neighbors) {
            if (isValid(nei.x, nei.y, grid) && nei.value == '1') {
                dfs(nei, graph, grid);
            }
        }

        // 
    }
    private Set<Vertex> buildGraph(char[][] grid) {
        Set<Vertex> graph = new HashSet<>();
        for (int x = 0; x < grid.length; x++) {
            for (int y = 0; y < grid[0].length; y++) {
                Vertex cur = new Vertex(x, y, grid[x][y]);
                graph.add(cur);
            }
        }
        for (Vertex vertex: graph) {
            for (int[] dir: DIRT) {
                int neiX = vertex.x + dir[0];
                int neiY = vertex.y + dir[1];
                if (isValid(neiX, neiY, grid)) {
                    for (Vertex nei: graph) {
                        if (nei.x == neiX && nei.y == neiY) {
                            vertex.neighbors.add(nei);
                        }
                    }
                }
            }
        }
        return graph;
    }
    private boolean isValid(int x, int y, char[][] grid) {
        return x >= 0 && x < grid.length && y >= 0 && y < grid[0].length;
    }
    private static final int[][] DIRT = new int[][]{{-1, 0},{1, 0}, {0,1}, {0, -1}};
}
```

#### &#x20;Method 2 DFS & BFS for maximum area of island







