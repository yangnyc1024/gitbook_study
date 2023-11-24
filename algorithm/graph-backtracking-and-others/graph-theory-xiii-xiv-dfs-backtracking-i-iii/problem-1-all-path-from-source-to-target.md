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



```java
public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
    List<List<Integer>> result = new ArrayList<>();
    if (graph == null || graph.length == 0) {
        return result;
    }
    List<Integer>

}
```
