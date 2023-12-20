# Basic



### Use case 1:所有解问题or all paths

所有解问题：all possible XXX--> 暴力解的根源



**明确backtracking问题里面，所谓的一个点允许多次是什么意思？**

* alll path problem里，我们不允许同一个node在同一条path上使用多次，<mark style="color:blue;">但是我们允许同一个node在不同path上使用多次</mark>
* backtracking每个点有可能被访问多次，但within一条path里的每一个点最多访问一次
* DFS Mark Visited需不需要mark visited呢？<mark style="color:blue;">yes mark的是同一条路径上，这个点有没有被使用过</mark>



<mark style="color:blue;">**Discuss吃吐守恒，**</mark>**什么时候要吐呢？backtracking的时候，回溯的时候**

* 这条路径已经遍历完，准备回去尝试其他路径的时候



**Recursion，Pure Recursion，Backtrack，DFS这四个词什么关系？**

* pure recursion and dfs both implemented in reucrsion way, their difference is 构建解的顺序不一样
* pure recursion from bottom to top, dfs backtracking from top to bottom
* backtrack is the behavior of DFS：一定有从一个分支回去再访问另一个分支

**DFS MarkVisited One: Reachable/ Connectivity**

```java
enum State {
    UNVISITED, VISITED
}
class Node {
    State state = State.UNVISITED;
    List<Node> neighbors;
}

private void DFSMarkVisistedOne(Node v) {
    if (v.state == State.VISITED) {
        return;
    }
    v.state = VISITED;
    for (Node nei: v.neighbors) {
        DFSMarkVisitedOne(nei);
    }
}
```

**DFS MarkVisited Three: Backtracking 针对use case 1：找到所有可能的路径/Solution**

```java
enum State {
    UNVISITED, VISITED
}

class Node {
    State state = State.UNVISITED;
    List<Node> neighbors;
}
private void DFSMarkVisitedThree(Node v) {
    if (v.state == State.VISITED) {
        return;
    }
    v.state = VISITED;
    for (Node nei: v.neighbors) {
        DFSMarkVisitedThree(nei);
    }
    v.state = UNVISITED;
}
```

**Backtracking High Level：说完high level心中有code能分析复杂度**

* Step 1: 什么是一个解？
* Step 2: 如何构建一个解？
  * 每一层是什么？
  * 分支是什么？
  * 在哪收集解呢？

### Use Case 2： 解的存在性问题：存不存在一个解，有没有一个解

* 你问我存不存在一个解
* 我只能找所有解，如果我遇到了一个解，那就存在
* 但是题目本身没有让你求所有解

**Apply 剪枝：剪枝本身就是所有DFS3的考点**

* 在use case 1里该剪的就剪
* 只要找到了一个解，我就直接return不再遍历其他解
* inplementation level：带return type的backtracking
* return type：boolean是否存在一个解

```java
//psudo code: return type：在这个分支下，能不能找到解
private boolean DFS() {
    if () {
        return true;
    }
    for (all branches) {
        if (DFS(this branch) == true) {
            return true;
        }
    }
    return false;
}


enum State {
    UNVISITED, VISITED
}

class Node {
    State state = State.UNVISITED;
    List<Node> neighbors;
}
private boolean DFSMarkVisitedThree(Node v) {
    if (v.state == State.VISITED) {
        return false;
    }
    if (condition reached) {
        return true;
    }
    v.state = VISITED;
    for (Node nei: v.neighbors) {
        if (DFSMarkVisitedThree(nei)) {
            return true;
        }
    }
    v.state = UNVISITED;
    return false;
}
```
