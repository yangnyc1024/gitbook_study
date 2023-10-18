# Question 0 Traversal & Reachable模版

## Graph Node

```java
// Some code
class GraphNode {
    int id;
    List<GraphNode> neighbors;
    
    // assume the graphNode has already overridden hashCode(), equals(), toString();
    @Override
    public int hashCode(){
    
    }
    
    @Override
    public int equals() {
    }
    
    @Override
    public int toString() {
    }
}
```

## DFS对点的遍历

1. <mark style="color:blue;">一点出发，遍历到我们能遍历到的所有点</mark>

* 每个点可能被到达多次（环，多个父亲节点）
* Logic
  * 如果访问到当前的点，赶紧回头（不访问）
    * 否则，访问这个点，同时继续访问他的neighbors

```java

public List<GraphNode> DFSMarkVisitedOne(GraphNode start) {
    List<GraphNode> result = new ArrayList<>();
    Set<GraphNode> visited = new HashSet<>();
    DFSMarkVisitedOne(start, visited, result);
    return result;
}

private void DFSMarkVisitedOne(GraphNode curNode, Set<GraphNode> visited, List<GraphNode> result) {
    if (visited.contains(curNode)) {
        return;
    }
    visited.add(curNode);
    result.add(curNode);
    for (GraphNode nei: curNode.neighbors) {
        DFSMarkVisitedOne(nei, visited, result);
    }
}
```

2. <mark style="color:blue;">对于不联通图中有多个联通分量</mark>

* 要想遍历出所有的点，不可能从一个点出发
* 有几个联通分量，需要从几个点出发/需要出发几次，每一次从一个新的connect里挑选一个点出发

```java
// Some code

//有多少个联通分量
public int DFSMarkVisitedOne(List<GraphNode> nodeList) {

    Set<GraphNode> visited = new HashSet<>();
    int numberOfConnectedComponent = 0;
    for (GraphNode eachNode : nodeList) {
        if (!visited.contains(curNode)) {
            DFSMarkVisitedOne(curNode, visited);
            numberOfConnectedComponent++;
        }
    }
    return numberOfConnectedComponent;
}

private void DFSMarkVisitedOne(GraphNode curNode, Set<GraphNode> visited, List<GraphNode> result) {
    if (visited.contains(curNode)) {
        return;
    }
    visited.add(curNode);
    result.add(curNode);
    for (GraphNode nei: curNode.neighbors) {
        DFSMarkVisitedOne(nei, visited, result);
    }
}
```

Follow Up:

* 联通分量里最多的点是多少？
  * 记录每个联通分量里的点数，每次出发都得记录一下这次出发遍历；轭多少点
  * Maximum it
* 有多少个联通分量包含最多的点？
  * 实际记录下来这个联通分量有哪些点，有多少点
  * 筛选出拥有最多联通分量点数的所有联通分量



## BFS对点的遍历

**同样的逻辑，同样的操作(expansion and generation), 注意防止多次generate或者expand**

#### 去重的位置

* <mark style="color:blue;">既可以在exapansion的时候去重。</mark>
  * 允许一个点被generate多次，但是只对第一次exapnd的这个点进行访问，后面我发现再expand到已经visited过的node，直接ignore
* <mark style="color:blue;">也可以在Generation的时候去重。</mark>
  * 不允许一个点被generate多次，每一个点如果你最多只放进queue一次，那么它也就至多被拿出来一次
* <mark style="color:blue;">优缺点比较</mark>
  * Expansion去重：必然正确，但是缺点为空间复杂度高（queue size不能保证最大的O(V)）
  * Generation去重：空间好，Queue的wize至多不会超过O(V)，缺点是<mark style="color:orange;">不一定正确（connectivity and reachable problem一定正确，但是shortest path and etc 不一定正确）</mark>

```java
public List<GraphNode> BFS(GraphNode start) {
    List<GraphNode> result= new ArrayList<>();
    Set<GraphNode> visited = new HashSet<>();
    Deque<GraphNode> queue = new ArrayDeque<>();
    
    queue.offer(start);
    visited.add(start);
    
    while (!queue.isEmpty()) {
        GraphNode curNode = queue.poll();
        result.add(curNode.id);
        for (GraphNode nei: curNode.neighbors) {
            if (!visited.contains(nei)) {
                queue.offer(nei);
                visited.add(nei);
            }
        }
    }
    return result;
}
```

## DFS对connection& reachable

```java
public boolean DFSMarkVisitedOne(GraphNode start, GraphNode target) {
    Set<GraphNode> visited = new HashSet<>();
    return DFSMarkVisitedOne(start, visited, target);
}
// boolean means 从curNode是否能到target
private boolean DFSMarkVisitedOne(GraphNode curNode, Set<GraphNode> visited,  GraphNode target){
    if (visited.contains(curNode)) {
        return false;
    }
    visited.add(curNode);
    if (curNode.equals(target)) { // 注意这里是用equals
        return true;
    }
    for (GraphNode nei: curNode.neighbors) {
        if (DESMarkVisitedOne(nei, visited, target)) {
            return true;
        }
    }
    return false;
} 
```







## BFS对connection& reachable

```java
// BFS all in Generation;
public boolean BFS(GraphNode start, GraphNode target) {
    Set<GraphNode> visited = new HashSet<>();
    Deque<GraphNode> queue = new ArrayDeque<>();
    
    
    queue.offer(start);
    visited.offer(start);
    
    while (!queue.isEmpty()) {
        GraphNode curNode = queue.poll();
        for (GraphNode nei: curNode.neighbors) {
            if (nei.equals(target)) {
                return true;
            }
            if (!visited.contains(nei)) {
                visited.add(nei);
                queue.offer(nei);
            }
        }
    }
    return false; // unreachable

}


// BFS all in Expansion

public boolean BFS(GraphNode start, GraphNode target) {
    Set<GraphNode> visited = new HashSet<>();
    Deque<GraphNode> queue = new ArrayDeque<>();
    
    while (!queue.isEmpty()) {
        GraphNode curNode = queue.poll();
        if (visited.contains(curNode)) {
            continue;
        }
        if (curNode.equals(target)) {
            return true;
        }
        for (GraphNode nei: curNode.neighbors) {
            queue.offer(nei);
        }
    }    
}
```

## 对边的遍历：Backtracking(see the future section)

## The Representation of the Graph in these questions

### 面试中图论的基本要素

* 图论面试的第零步: this is actually a graph problem (model)
* 面试中第一步： graph building (u - v) 构图请单独写一个helper function



### 题库喜欢的表示方法1: int\[]\[] graph

* list of all edges,甚至可以是权重
* 本质就是更新这两个map
  * Map\<Integer, Map\<Integer, Integer>> graph = new HashMap<>()
    * Map\<u, Map\<v, weight>> graph
  * Map\<Integer, Integer> IndegreeMap = new HashMap<>();
    * Map\<u, indegree>

#### Case 1: Telling me is an Undirected Graph

<pre class="language-java"><code class="lang-java"><strong>// 这两行声明再其他函数里
</strong><strong>Map&#x3C;Integer, Map&#x3C;Integer, Integer>> graph = new HashMap&#x3C;>();
</strong><strong>Map&#x3C;Integer, Integer> IndegreeMap = new HashMap&#x3C;>();
</strong><strong>
</strong><strong>private void buildGraph(int[][] edges, Map&#x3C;Integer, Map&#x3C;Integer, Integer>> graph, Map&#x3C;Integer, Integer> IndegreeMap) {
</strong><strong>    for (int[] edge: edges) {
</strong><strong>        int u = edge[0];
</strong><strong>        int v = edge[1];
</strong><strong>        int weight = edge[2];
</strong><strong>        //两边都要放
</strong><strong>        graph.putIfAbsent(u, new HashMap&#x3C;>());
</strong><strong>        graph.putIfAbsent(v, new HashMap&#x3C;>());
</strong><strong>        graph.get(u).put(v, weight);
</strong><strong>        graph.get(v).put(u, weight);
</strong><strong>    }
</strong><strong>}
</strong></code></pre>

#### Case 2: Telling me is a Directed Graph

```java
// 这两行声明再其他函数里
Map<Integer, Map<Integer, Integer>> graph = new HashMap<>();
Map<Integer, Integer> IndegreeMap = new HashMap<>();

private void buildGraph(int[][] edges, Map<Integer, Map<Integer, Integer>> graph, Map<Integer, Integer> IndegreeMap) {
    for (int[] edge: edges) {
        int u = edge[0];
        int v = edge[1];
        int weight = edge[2];
        // u --> v u里面加v，但是v的入度更新
        graph.putIfAbsent(u, new HashMap<>());
        graph.get(u).put(v, weight);
        IndegreeMap.put(v, IndegreeMap.getOrDefault(v, 0) + 1);
    }
}
```

### 题库喜欢的表达方法2: int\[]\[] matrix 扔给你个地图

* example: grid/matrix == \[\[0   0 (0,1)   1   1  ], \[0 1(1, 1)  1   2], \[0    1   1  0(2,3)], \[0  0  1  0]]
* 坐标当点：
  * 方向：二方向/四方向/八方向

#### Question 1: 用每个点的matrix坐标表示一个node会不会超界

```java
private boolean isValid(int[][] grid, int i, int j) {
    return i >= 0 && i < grid.length && j >=0 && j < grid[0].length;
}

// with blocker && visited[i][j] version
private static final int BLOCKER = 1;
private boolean isValid(int[][] grid, int i, int j) {
    return i >= 0 && i < grid.length && j >=0 && j < grid[0].length && grid[i][j]!= BLOCKER && !visited[i][j];
}
```

#### Question 2 方向怎么办?



```java
// Case 1: 二方向（随机选两个）或者四方向
private static final int[][] DIRS = {{-1, 0}, {1, 0}; {0, -1}; {0, 1}};
// 上，下，左，右

// Case 2: 八方向
private static final int[][] DIRS = {
 {-1, 0}, {1, 0}, {0, -1}, {0, 1},
 {-1, -1}, {1, -1}, {-1, 1}, {1, 1};
}
// 上，下，左，右，左上，左下，右上，右下

// Case 3: 跳马八方向
private static final int[][] DIRS = {
 {-2, -1}, {-2, 1}, {-1, -2}, {-1, 2},
 {1, -2}, {1, 2}, {2, -1}, {2, 1};
}
```



#### Use Case: 给你一个点(curX, curY) 能不能访问所有邻居

```java
public void printAllNeighbors(int[][] grid, int curX, int curY, boolean[][] visited) {
    for (int[] dir: DIRS) {
         int neiX = curX + dir[0];
         int neiY = curY + dir[1];
         if (isValid(grid, neiX, neiY, visited)) {
              System.out.println(grid[neiX][neiY]);
              // DFS(neiX, neiY,...) or Queue.offer...
         }
    }

}
```
