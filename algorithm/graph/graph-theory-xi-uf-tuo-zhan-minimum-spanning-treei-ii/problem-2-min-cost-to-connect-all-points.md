# Problem 2: Min Cost to Connect All Points

```java
public int minCostToConeectAllPoints(int[][] points) {
    int result = 0;
    // int[]: {dist(a, v), a, b}
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
    for (int i = 0; i < points.length; i++) {
        for (int j = i+ 1; j < points.length; j++) {
            minHeap.offer(new int[] {findDist(points,i,j), i, j});
        
        }
    }
    int count = 0;
    UnionFind uf = new UnionFind(points.length);
    
    while (count < n -1) {
        int[] edge = minHeap.poll();
        int weight = edge[0];
        int u = edge[1];
        int v = edge[2];
        if (uf.find(u) != uf.find(v)) {
            result += weight;
            count++;
            uf.union(u, v);
        }
    }
    return result;
}


private int findDist(int[][] points, int a, int b) {
    return Math.abs(points[a][0] - points[b][0] + Math.abs(points[a][1] - points[b][1]));

}

class UnionFind{ //一般可以单独出来，这里还可以加union by weight增加速度
    int[] laoda;
    public UnionFind(int n) {
        this.laoda = new int[n];
        for (int i = 0; i < n; i++){
            laoda[i] = i;
        }
    }
    public int find(int a) {
        return laoda[a] = a == laoda[a]? a: find(laoda[a]);
    }
    public void union(int a, int b) { // 从a到b
        int alaoda = find(a);
        int blaoda = find(b);
        if (alaoda != blaoda) {
            laoda[alaoda] = blaoda;
        }
    }
}
```
