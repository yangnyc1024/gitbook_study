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

## The  Representation of the Graph in these questions
