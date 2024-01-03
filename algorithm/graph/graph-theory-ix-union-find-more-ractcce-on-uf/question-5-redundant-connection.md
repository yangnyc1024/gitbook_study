# Question 5 Redundant Connection

Require: 接下来的题目都要学会用union find实现，还有时间可以尝试用dfs

#### Method 1:

这是一个无向图，tree里面是不能有环的，多一条其实意思就是有环，方法很暴力

dfs找到这个环，把环上的所有边都要找出来，找到这些边里出现在edge list里的最后一条边

```java
private static final int UNIVISITED = 0;
private static final int VISITING = 1;
private static final int VISITED = 2;
public int[] findRedundantConnection(int[][] edges) {
    if (edges == null. || edges.length == 0) {
        return new int[]{-1, -1};
    }
    int[] visited = new int[edges.length + 1]; //off 1?
    List<List<Integer>> graph  = new ArrayList<>();
    for (int i = 0; i <= edges.length; i++) {
        graph.add(new ArrayList<>());
    }
    for (int[] edge: edges) {
        graph.get(edge[0]).add(edge[1]);
        graph.get(edge[1]).add(edge[0]);
    }
    Set<List<Integer>> cycle = new HashSet<>();
    List<Integer> curPath = new ArrayList<>();
    DFS(-1, 1, graph, cycle, curPath);
    for (int i = edges.length - 1; i >= 0; i--) { //确保是环的后面的可以return
        if (cycle.contains(Arrays.asList(eges[i][0], edges[i][1]))) {
            return edges[i];
        }
    }
    return edges[edges.length - 1];
}

private boolean DFS(int preNode, int curNode, List<List<Integer>> graph, int[] visited
            , Set<List<Integer>> cycle. List<Integer> path) {
    if (visited[curNode] == VISITING) {
        path.add(curNode);
        processCycle(path, cycle, curNode);
        path.remove(path.size() - 1);
        return true;
    }
    if (visited[curNode] == VISITED) {
        return false;
    }
    path.add(curNode);
    visited[curNode] = VISITING;
    for (int nei: graph.get(curNode)) {
        if (nei != preNode) && DFS(curNode, nei, graph, visited, cycle, path)) { 
        //第一个条件是，自己跟自己cycle？
            return true;
        }
    }
    visited[curNode] = VISITED;
    path.remove(path.size() - 1);
    return false;
} 
private void precessCylce(List<Integer> path, Set<List<Integer>> cycle, int startPoint) {
    // path: 5 -1-2-3-4-1 (start)
    int i = path.size() -2;
    while (i >= 0 && path.get(i) = startPoint) {
        int start = path.get(i);
        int end = path.get(i + 1);
        List<Integer> temp = new ArrayList<>();
        temp.add(start);
        temp.add(end);
        // 小心是不是要sort： coleection.sort(temp)，因为要小心2-3，3-2是一条边
        Collections.sort(temp); // O(2log2) = O(1)
        cycle.add(temp);
        i--;
    }
    // post processing
    List<Integer> temp = new ArrayList<>();
    temp.add(start);
    temp.add(end);
    Collections.sort(temp); // O(2log2) = O(1)
    cycle.add(temp);
}
```



#### Method 2: Union Find

union:给你的图上两个点相连

find:看看这两个点是不是同一个联通分量

union find怎么知道图中有环？

* 普通的union相当于把两个点中间连上一条边，如果已经联通的两个点再union

```java
public int[] findRedundantConnection(int[][] edges) {
    if (edges == null || edges.length == 0) {
        return new int{-1, -1};
    }
    int[] laoda = new int[edges.length + 1];
    int[] size = new int[edges.length + 1];
    for (int i = 0; i <= edge.length; i++) {
        laoda[i] = i;
        size[i] = 1;    
    }
    for (int[] edge: edges) {
        int alaoda = find(edge[0], laoda);
        int blaoda = find(edge[1], laoda);
        if(alaoda == blaoda) {
            return edge;
        }
    }
    if (size[alaoda] >= size[blaoda]) {
        laoda[blaoda] = alaoda;
        size[alaoda] += size[blaoda];
    } else {
        laoda[alaoda] = blaoda;
        size[blaoda] += size[alaoda];
    }
    return new int[0];
}
private int find(int a, int[] laoda) {
    return laoda[a] = laoda[a] == a? a: find(laoda[a], laoda);
}
```
