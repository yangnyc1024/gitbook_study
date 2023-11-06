# Problem 6 Trapping Rain Water II





这道题最坑的部分是，一个是高度，一个是它这个点的蓄水高度

* （普及）高度是给里面点的蓄水高度准备的
* 蓄水高度是根据周围的点的（普及高度）高度来说



关键点

* 普及高度，只可能升高，不可能变低
* 走的点是从最小的普及高度，
* 蓄水量 = max（普及高度 - 该点的高度，0）





generate 要做什么

* 计算neighbor的蓄水量
  * 蓄水量 = max（cur.普及高度 - cur.高度，0）
* update到neighbor为止的普及高度
  * <mark style="color:green;">cost 就是普及高度 ，所以neighbor.普及高度 = max (cur.普及高度， neighbor的高度) (since cur.普及高度>0) = cur.普及高度 + max(0， neighbor的高度 - cur.普及高度)</mark>
    * cost 就是普及高度
    * cost(开始的点（外围一圈最小点）， x.neighbor) = cost(开始的点， x) + cost (x, neighbor)
    * 所以edge上的weight应该是这玩意 max(0， neighbor的高度 - cur.普及高度)



````java

class Solution {
    public class Cell implements Comparable<Cell> {
        int x;
        int y;
        int cost;
        Cell (int x, int y, int cost) {
            this.x = x;
            this.y = y;
            this.cost = cost;
        }
        @Override
        public int hashCode() {
            int hashCode = this.x + 31;
            hashCode = hashCode * this.y  + 31;
            return hashCode;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null) return false;
            if (this.getClass() != obj.getClass()) {
                return false;
            }
            Cell that = (Cell) obj;
            return this.x == that.x && this.y == that.y;
        }
        @Override
        public int compareTo(Cell that) {
            int result = Integer.compare(this.cost, that.cost);
            int result_x  = Integer.compare(this.x, that.x);
            int result_y = Integer.compare(this.y, that.y);
            if (result == 0) {
                return result_x;
            }
            else if (result == 0 && result_x == 0) {
                return result_y;
            }
            return result;
        }
    }
    private final static int[][] DIRS = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    public int trapRainWater(int[][] heightMap) {
        // sanity check
        if (heightMap == null || heightMap[0] == null || heightMap.length == 0 || heightMap[0].length == 0) {
            throw new IndexOutOfBoundsException("out of bound");
        }
        int m = heightMap.length;
        int n = heightMap[0].length;

        // visited boolean matrix
        boolean[][] visited = new boolean[m][n];

        // bfs & dfs
        PriorityQueue<Cell> pq = new PriorityQueue<>();
        initializePQueue(pq, heightMap, m, n, visited);
        int result = 0;
        while (!pq.isEmpty()) {
            int size = pq.size();
            for (int i = 0; i < size; i++) {
                Cell cur = pq.poll();
                for (int[] dir: DIRS) {
                    int neiX = cur.x + dir[0];
                    int neiY = cur.y + dir[1];
                    if (!isValid(neiX, neiY, heightMap)) {
                        continue;
                    }
                    if (visited[neiX][neiY]) {
                        continue;
                    }
                    result += Math.max(0, cur.cost - heightMap[neiX][neiY]);
                    pq.offer(new Cell(neiX, neiY, Math.max(heightMap[neiX][neiY], cur.cost)));
                    visited[neiX][neiY] = true;
                }
            }
        }
        return result;
    }
    private boolean isValid(int x, int y, int[][] heightMap) {
        return x >= 0 && x < heightMap.length && y >= 0 && y < heightMap[0].length;
    }
    private void initializePQueue(PriorityQueue<Cell> pq, int[][] heightMap, int m, int n, boolean[][] visited) {
        for (int i = 0; i < m ; i++) {
            pq.offer(new Cell(i, 0, heightMap[i][0]));
            visited[i][0] = true;
            pq.offer(new Cell(i, n -1, heightMap[i][n - 1]));
            visited[i][n - 1]  = true;
        }
        for (int j = 0; j < n; j++) {
            pq.offer(new Cell(0, j, heightMap[0][j]));
            visited[0][j] = true;
            pq.offer(new Cell(m -1, j, heightMap[m - 1][j]));
            visited[m -1][j] = true;
        }
    }
}
```
````
