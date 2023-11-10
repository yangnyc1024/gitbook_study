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
  * 蓄水量 = max（<mark style="color:blue;">cur.普及高度 - neighbor.高度</mark>，0）
* update到neighbor为止的普及高度
  * <mark style="color:green;">cost 就是普及高度 ，所以neighbor.普及高度 = max (cur.普及高度， neighbor的高度) (since cur.普及高度>0) =</mark> <mark style="color:green;"></mark>_<mark style="color:green;">**cur.普及高度 + max(0，**</mark>** **<mark style="color:blue;">**neighbor.高度 - cur.普及高度**</mark><mark style="color:green;">**)**</mark>_
  * cost 就是普及高度
  * cost(开始的点（外围一圈最小点）， x.neighbor) = cost(开始的点， x) + cost (x, neighbor)
  * 所以edge上的weight应该是这玩意 max(0， neighbor的高度 - cur.普及高度)



```java


class Solution {
    class Element implements Comparable<Element> {
        int x;
        int y;
        int pujiHeight;
        public Element(int x, int y, int pujiHeight) {
            this.x = x;
            this.y = y;
            this.pujiHeight = pujiHeight;
        }
        @Override
        public int compareTo(Element other) {
            return Integer.compare(this.pujiHeight, other.pujiHeight);
        }
    }
    public int trapRainWater(int[][] heightMap) {
                // sanity check
        if (heightMap == null || heightMap.length == 0 || heightMap[0].length == 0) {
            return -1;
        }
        
        // initiation (result, graph, visited, minHeap, etc)
        int[] result = new int[]{0};
        boolean[][] visited = new boolean[heightMap.length][heightMap[0].length];
        PriorityQueue<Element> minHeap = new PriorityQueue<>();
        
        // bfs
        bfs(minHeap, heightMap, visited, result);
        
        // return result
        return result[0];
    }
    private static final int[][] dirs = new int[][]{{-1, 0}, {1,0}, {0, 1}, {0, -1}};
    private void bfs(PriorityQueue<Element> minHeap, int[][] heightMap, boolean[][] visited, int[] result) {
        // initial state
        initialState(minHeap, heightMap, visited);
        while (!minHeap.isEmpty()) {
            Element cur = minHeap.poll();
            for (int[] dir : dirs) {
                int neiX = cur.x + dir[0];
                int neiY = cur.y + dir[1];
                if (isValid(heightMap, neiX, neiY) && !visited[neiX][neiY]) {
                    int cost = Math.max(cur.pujiHeight - heightMap[neiX][neiY], 0);
                    result[0] += cost;
                    int neiPujiHeight = cur.pujiHeight + Math.max(heightMap[neiX][neiY] - cur.pujiHeight, 0);
                    Element neiElement = new Element(neiX, neiY, neiPujiHeight);
                    minHeap.offer(neiElement);
                    visited[neiX][neiY] = true;
                }
            }
        
        }
    }

    private void initialState(PriorityQueue<Element> minHeap, int[][] heightMap, boolean[][] visited) {
        // add the top and bottom row
        for (int i = 0; i < heightMap[0].length; i++) {
            minHeap.offer(new Element(0, i, heightMap[0][i]));
            minHeap.offer(new Element(heightMap.length - 1, i, heightMap[heightMap.length - 1][i]));
            visited[0][i] = true;
            visited[heightMap.length - 1][i] = true;
        }
        // add the left and right column
        for (int j = 0; j < heightMap.length; j++) {
            minHeap.offer(new Element(j, 0, heightMap[j][0]));
            minHeap.offer(new Element(j, heightMap[0].length - 1, heightMap[j][heightMap[0].length - 1]));
            visited[j][0] = true;
            visited[j][heightMap[0].length - 1] = true;
        }
    }
    private boolean isValid(int[][] heightMap, int x, int y) {
        return x >= 0 && x < heightMap.length && y >= 0 && y < heightMap[0].length;
    }
}

```
