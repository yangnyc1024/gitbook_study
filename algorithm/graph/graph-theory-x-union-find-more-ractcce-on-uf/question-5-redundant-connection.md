# Question 5 Redundant Connection

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
    DFS(-1, -1, graph, cycle, curPath);
    for (int i = edges.length - 1; i >= 0; i--) {
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
        // 小心是不是要sort： coleection.sort(temp)
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
