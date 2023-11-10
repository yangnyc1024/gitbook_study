---
description: Intro
---

# Intro

#### Kahn's Algorithm



#### Use Case

* 这个问题应该被什么顺序觉解
* 这个问题让你判断能不能被解决，给你的条件有没有矛盾==》 判断有向图中有没有环

#### Topological Sort最重要的点

* 定义dependecy， a---> b (b depends a)

#### 重要的概念：inDegree

* indegree\[]: how many edges are pointing to itself

#### topological sort和有无环的关系

* 有topological sort那就一定是有向无环图
* 没有topological sort有可能是无向图，不一定是有环（有向就没问题，无向不可以）



#### 怎么判断有无环

* 对于任意一个有方向，定义好dependency：
  * run topological sort algorithm
  * 如果排好序的点= 总点数 ok，无环

```markdown
// Some code
L <- Empty list that will contain the sorted elements
S <- Set of all nodes with no incoming edge

while S is not empty do
    remove a node n from S
    add n to L
    for each node m with an edge e from n to m do
        remove edge e from the graph
        if m has no other incoming edges then
            insert m into S
if graph has edges then
    return error(graph has at least one cycle)
else
    return L (a topologically sorted order)
```



#### BFS Queue装的点的物理意义？

* <mark style="color:purple;">当前优先级相同的点，所有入度为0的点。</mark>
* 实际情况
  * 先generate一堆点：所有入度为0的node
  * 每次从入度为0的点出发：
    * expand
    * exapnd一个入度为0点：加入拓扑排序
      * update所有我expand的这个点的dependency：
      * 我的neighbor node：<mark style="background-color:red;">indegree\[nei of curNode]--</mark>;
    * genereate:如果你发现update完了以后这个neighbors node indegree<mark style="color:purple;">变成0了，</mark><mark style="color:red;">就把它generate出来</mark>











### 基本Implementation

* 图representation: Map\<Node, List\<Node>/ Set\<Node>> graph
* inDegree:
  * int\[] inDegree (if Node is represnted by integer id)
  * Map\<Node, Integer> indegreeMap
* 最简单化，Set\<Node> allNodes 记录graph里所有的Node
* Queue: Deque\<Node> queue = new ArrayDeque<>();
* Topological Result: List\<Node> result

Step 1: 先generate所有入度为0的点

<pre class="language-java"><code class="lang-java">// Step 1: 先generate所有入度为0的点
for (Node: node: allNodes) {
    if (indegreeMap.get(node) == 0) {
        queue.offer(node);
    }
}


<strong>//Step 2: Do DFS
</strong>
while (!queue.isEmpty()) {
    Node cur = queue.poll();
    result.add(cur); //加入拓扑排序
    for (Node nei: graph.get(cur)) {
        indegreeMap.put(nei, indegreeMap.get(nei) - 1);
        if (indegreeMap.get(nei) == 0) {
            queue.offer(nei);
        }
    }
}

// Step 3: check 环
if (allNodes.size() != result.size()) {
    //有环，没有拓扑排序
}
</code></pre>

#### Question: 不联通的图，可不可以有拓扑排序？

* example A, B-> C, E-> F-> G
* yes, one of the valid topological sort: A, B, E, C, F, G

