# Problem 3: Optimize Water Distribution in a Village

Question 1: 这道题是个MST的题目吗？

Question 2: 区别点在于这道题可以自己大惊小怪？

* 有的店不需要别人联通了

主要的难点：我们怎么把这道题转化成一个母题：直接构造最小生成树

* 大家的思考：水源何在
* 打井和水源的关系：能不能假想一个水源==》我可以把水源看成一个点



Step1: Dummy Node for wells\[i]

Step2: Sort all edges then kruskal algorithm

Step3: 在这个修改过的图中做MST算法和普通的构建结果有什么区别吗？

Question：怎么处理这个dummyNode？

* 这样的话，我们的MST不是build基于加过0这个点的MST了吗？会不会我们include的n-1条边没法链接到所有的村庄呢？
* 回答，完全不用处理
* 我们这道题目的是为了连接到所有的村庄吗？我们的目的是给每个村通上谁，如果你构建这个n-1条边里有一些便是跟dummyNode链接，说明这些村庄打井更合算



Thinking: 哪些村庄需要自己打井，哪些是需要引水

```java
public int minCostToDistributeWater(int n, int[] wells, int[][] pipes) {
    List<int[]> allEdges = new ArrayList<>();
    addAddEdges(n, wells, pipes, allEdges);
    return kruskals(n, allEdges);
}

private int kruskals(int n, List<int[]> allEdges) {
    // step 1: sort all the edges
    Collections.sort(allEdges, (a,b) -> Integer.compare(a[2], b[2]));
    int minCost = 0;
    int processedEdges = 0;
    
    // step 2: apply kruskals
    UnionFind uf = new UnionFind(n + 1);
    for (int[] edge: allEdges) {
        //其实也可以改变unionfind里的union这个方法，本题已经apply
        int u = edge[0];
        int v = edge[1];
        int weight = edge[2];
        if (uf.union(u, v)) {
            preocessedEdges++;
            minCost += weight;
            if (precessedEdges == n) { // 保证n个村有水
                break;
            }
        }
    }
    return minCost;
}


private void addAddEdges(int n, int[] wells, int[][] pipes, List<int[]> allEdges) {
    // 所有从水源出去的边全部搞定
    for (int i = 0; i < n; i++) {
        allEdges.add(new int[]{0, i + 1, wells[i]});
    }
    for(int[] pipe: pipes) {
        addEdges.add(pipe);
    }
}
```

Tips: Union 的return type是可以用的！： 能不能union代表了你想union的这两个人是不是同一个帮拍的可以做的事把return type赋予一个物理意义：会不会构成环

void union(int a, int b)==> boolean union(int a, int b):我应不应该去union这两个点
