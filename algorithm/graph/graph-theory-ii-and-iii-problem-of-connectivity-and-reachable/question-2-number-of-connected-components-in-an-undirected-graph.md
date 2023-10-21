# Question 2 Number of connected Components in an Undirected Graph

## Summary

### Step 1: State the Problem 归大类

* this is a graph problem
* I would like to model the problem to a graph problem

### Step 2: Build Graph

* vertex: node
* edge: undirected edges
* assume that <mark style="color:red;">**no duplicate edges**</mark> will appear in edges ==> <mark style="color:red;">Map\<Integer, List\<Integer>></mark>

### Step 3 & 4: what problem--> really solve which problem?

* so the problem is asking me to find out how many <mark style="color:red;">**connected components**</mark> are there in the graph built
* 每一次从一个没访问过的点出发都能遍历完一个新的联通分量的所有点：
* 我从几个点出发了，我就有几个联通分量
* numbersOfConnectedComponent有几个联通分量
* Therefore this is a traversal(reachable) problem in graph

### Step 5: propose 算法对边选择最优

* dfs & bfs



```java
class Solution {
// assumption: no duplicate edges
    public int countComponents(int n, int[][] edges) {
        Map<Integer, List<Integer>> map = buildGraph(edges);
        boolean[] visited = new boolean[n];
        int numberOfConnectedComponent = 0;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(i, visited, map);
                numbersOfConenectedComponent++;
            }
        }
        return numberOfConnectedCompnent++;
    }
    private void dfs (int cur, boolean[] visited, Map<Integer, List<Integer>> map) {
        if (visited[cur]) {
            return;
        }
        visited[cur] = true;
        List<Integer> neighbors = map.get(cur);
        if (neighbors != null) {
             for (int nei: neighbors) {
                 dfs(nei, visited, map);
             }
        }
    }
    private Map<Integer, List<Integer>> buildGraph(int[][] edges) {
        Map<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            map.putIfAbsent(u, new ArrayList<>());
            map.putIfAbsent(v, new ArrayList<>());
            map.get(u).add(v);
            map.get(u).add(v);
        }
        return map;
    }
}
```

```java
// Some code


class Solution {
    // assumption: no duplicate edges
    public int countComponents(int n, int[][] edges) {
        Map<Integer, List<Integer>> map = buildGraph(edges);
        boolean[] visited = new boolean[n];
        int numberOfConnectedComponent = 0;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                bfs(i, visited, map);
                numberOfConnectedComponent++;
            }
        }
        return numberOfConeectedComponent++;
    }
    private void dfs(int curNode, boolean[] visited, Map<Itneger, List<Integer>> map) {
        Queue<Integer> queue = new ArrayQueue<>();
        queue.offer(curNode);
        visited[curNode] = true;
        // if the node has not been visited, go bfs, count++
        while (!queue.isEmpty()) {
            int cur = queue.poll();
            List<Integer> neighbors = map.get(cur);
            if (neighbors != null) {
                for (int nei: neighbors) {
                    if (!visited[nei]) {
                        queue.offer(nei);
                        visited[nei] = true;
                    }
                }
            }
        } 
    
    }
    private Map<Integer, List<Integer>> buildGraph(int[][] edges) {
        Map<Integer, List<Itneger>> graph = new HashMap<>();
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.putIfAbsent(u, new ArrayList<>());
            graph.putIfAbsent(v, new ArrayList<>());
            map.get(u).add(v);
            map.get(v).add(u);
        }
        return map;
    }
}
```
