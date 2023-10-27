# Side Topic: 如何在图中判断是否有环

## 有向图

* bfs拓扑排序(always covered)
* dfs markVisiting Two
  * 对点的状态分类增加
  * visited & unVisited  VS visited & unVisited& visiting
* Union Find
  * see previous
  * union 到两个已经同样老大的点



```java
enum State {
    UNVISITED, VISITED, VISITTING;
}
class Node{
    int id;
    State state;
    List<Node> neighbors;
    public Node(int id) {
        this.id = id;
        this.state = State.UNVISITED;
    }
    // this class already overridden the util method 
    // such as hashCode(), equals(), toString();
}
// teturn type:是不是从这个点出发可以发现一个环
public boolean DFSMarkVisitedTwo(Node cur) {
    if (cur.state == State.VISITED) {
        return false; //理解：上次来这个点都没有找到环，这次来不用来了肯定也找不到
    }
    if (cur.state == State.VISITING) {
        //理解:你其实是在到达cur以后，在沿着边的顺序防伪cur的neighbor的过程中居然又回到了cur
        System.out.println("Cycle Detected");
        return true;
    }
    // 理解：现在cur的state一定是unvisited
    cur.state = State.VISITING:
    for (Node nei : cur.neighbors) {
        if (DFSMarkVisited(nei) == true) {
            //理解：从我某一个neighbor出发能找到环，那就说明这个图里面有环，不用再看我的其他neighbor了
                return true;
        }
    }
    cur.state = VISITED;
    // 理解:说明从我出发肯定没有环
    return false;
}
```

In real practice

```java
private static final int UNISITTED = 0;
private static final int VISITING = 1;
private static final int vISITED = 2;
```

## 无向图

* XXXXXbfs拓扑排序(always covered)
* Union Find
  * see previous
  * union 到两个已经同样老大的点
* dfs markVisiting One Modified:
  * 沿着一个方向走，不回头，如果你能走到一个走过的点

如果是非联通图，从每个联通块出发就好了

```java
public void DFSMarkVisitedOneModified(Node start) {
    Set<Node> visited = new HashSet<>();
    return DFSModified(start, null, visited);
}
private boolean DFSModified(Node cur, Node prevNode, Set<Node> visited) {
    if (visited.contains(cur)) {
        System.out.println("There is a cycle");
        return true;
    }
    visited.add(cur);
    for (Node nei: cur.neighbors) {
        if (!nei.equals(prevNode)) {
            if (DFSModified(nei, cur, visited)) {
                return true;
            }
        }
    }
    return false;
}
```



