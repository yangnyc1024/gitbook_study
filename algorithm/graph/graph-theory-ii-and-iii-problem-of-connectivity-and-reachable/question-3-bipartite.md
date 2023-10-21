# Question 3 Bipartite

染色问题本质上就是遍历问题

遍历一遍这张图，真的进行染色，如果你能顺利的染色完成，那就是二分图，不然起了冲突就不是二分图



遍历到一个点的时候，应该已经知道这个点应该是什么颜色了

* case 1如果这个点还没有染色，
  * 染色 +继续遍历
* case 2如果这个点已经染色
  * case 2.1 如果染色的颜色和应该染色的颜色一致，
    * 那就ok，continue
  * case 2.2 如果这个点染的颜色和应该染的冲突
    * return fasle不是二分图



```java
class Solution {
    public boolean isBipartite(List<GraphNode> graph) {
        Map<GraphNode, Integer> visited = new HashMap<>();
        for (GraphNode node: graph) {
            if (visited.containsKey(node)) {
                continue;
            }
            if (!bfs(node, visited)) {
                return false;
            }
        }
        return true;
    }
    private boolean bfs(GraphNode node, Map<GraphNode, Integer> visited) {
        Deque<GraphNode> queue = new ArrayDeque<>();
        queue.offer(node);
        visited.put(node, 1);
        while(!queue.isEmpty()) {
            GraphNode curNode = queue.poll();
            int curGroup = visited.get(curNode);
            int neiGroup = - curGroup;
            for (GroupNode nei: curNode.neighbors) {
                if (visited.containsKey(nei)) {
                    if (visited.get(nei) == curGroup) {
                        return false;
                    }
                    else {
                        visited.put(nei, neiGroup);
                        queue.offer(nei);
                    }
                }
            }
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isBipartite(List<GraphNode> graph) {
        Map<GraphNode, Integer> visited = new HashMap<>();
        for (GraphNode node: graph) {
            if (visited.containsKey(node)) {
                continue;
            }
            if (!dfs(node, visited, 1)) {
                return false;
            }
        }
        return true;
    }
    private boolean dfs(GraphNode node, Map<GraphNode, Integer> visited, int color) {
        if (visited.containsKey(node)) { 
            int curGroup = visited.get(node);
            if (curGroup == color) {
                return true;
            }
            else {
                return false;
            }
            visited.put(node, color);
            for(GraphNode nei: node.neighbors){
                if (!dfs(nei, visited, -color)) {
                    return false;
                }
            }
            return true;
        }
    
    
    }
}
```
