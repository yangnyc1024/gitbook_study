---
description: https://leetcode.com/problems/all-paths-from-source-to-target/
---

# Problem 1 All Path From Source to Target

High Level:

* 什么是一个解：One path from node 0 to node n -1 is a solution
* Path: Collection of nodes,  点与点之间必须连续



How to generate one solution

* recursion tree(how do you generate all the solutions)
* what is in the recursion tree each level?
  * add one node in each level
* what are branches?
  * which edge of this node will you select
* total number of levels?
  * total number of nodes

TC & SC

* O(n^n), O(n)



**经验（DFS一定有一个主函数）**

* &#x20;Step 1: 题目需要return什么我们就创建什么
* Step 2: Corner Case 不满足直接return第一步构建的结果
* Step 3: 构建当前层的解的容器，主要是观察第一步创建结构
  * List\<List\<Integer>> result ==> List\<Integer> current
  * List\<String> result ==> StringBuilder current
* Step 4: 打工的，层数的信息（level? currentNode?）
* Step 5: 把所有建出的信息都入DFS function
* Step Last：return第一步创建的结果





#### Method 1(在expand的时候mark visited)

```java
public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
    List<List<Integer>> result = new ArrayList<>();
    if (graph == null || graph.length == 0) {
        return result;
    }
    List<Integer> current = new ArrayList<>();
    boolean[] visited = new boolean[graph.length];
    int curNode = 0;
    dfs(curNode, graph, result, current, visited);
    return result
}
// recursion tree implementation
// int curNode: 当前我站在哪个点上
private void dfs(int curNode, int[][] graph, List<List<Intger>> result, List<Integer> current, boolean[] visited) {
    if (curNode == graph.length - 1) {
        current.add(curNode);
        result.add(new ArrayList<>(current));
        current.remove(current.size() - 1);
        return;
    }
    current.add(curNode);
    visited[curNode] = true; 
    for (int nei: graph[curNode]) {
        if (visited[nei]) {
            continue;
        }
        dfs(nei, graph, result, current, visited);
    }
    current.remove(current.size() - 1);
    visited[curNode] = false;
}

// 这题可以不mark visited ，因为这里是directed acyclic graph（DAG）:题目已经明确说明了是一个有向无环图，也就是说我们沿着方向走，只要没有自环是不会走出环的。
// 不过从物理意义上来说，应该是mark visited
```

```java

class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> ret = new ArrayList<>();
        if (graph == null) return ret;
        List<Integer> curResult = new ArrayList<>();
        curResult.add(0);
        int[] visited = new int[graph.length];
        visited[0] = 1;
        helper(graph, curResult, visited, ret, 0);
        return ret;
    }
    private void helper(int[][] graph, List<Integer> curResult, int[] visited, List<List<Integer>> ret, int curPosition) {
        // base case
        if (visited[visited.length - 1] == 1) {
            ret.add(new ArrayList<>(curResult));
            return;
        }


        // recursion rule
        for (int possVisit : graph[curPosition]) {
            if (visited[possVisit]!= 1) {
                curResult.add(possVisit);
                visited[possVisit] = 1;
                helper(graph, curResult, visited, ret, possVisit);
                curResult.remove(curResult.size() - 1);
                visited[possVisit] = 0;
            }
        }
    }
}

```
