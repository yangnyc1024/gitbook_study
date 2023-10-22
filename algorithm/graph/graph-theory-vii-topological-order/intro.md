---
description: Intro
---

# Intro

Kahn's Algortihm





#### 算法：BFS Queue装的点的物理意义： 当前优先级相同的点，所有入度为0的点。

* 先generate







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
