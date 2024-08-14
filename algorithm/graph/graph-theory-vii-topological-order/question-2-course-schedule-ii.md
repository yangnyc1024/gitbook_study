# Question 2 Course Schedule II



#### Compare the previous question

* 刚才是问存不存在一个valid topological sort: 这个follow up是问我们一个具体的一个valid topological sort
* public int\[] findOrder(int numCourses, int\[]\[] \[rerequisites) {}
* 定义method是面试里的一个步骤，candidate有权利也应该自己定义自己的API
* 写代码
  * 解释代码第一步就是解释和定义
  * 函数前面input + output + function能做什么
* 请定义对自己最有利的定义，比如
  * 如果面试过说了，图可以自己定义形式
  * return type自己想OJ上的return有时候是故意制造麻烦

````java
```java
```java
/*
clarification:

assumption:

high level:
- graph problem, topological order problem, bfs/ dfs

middle level:
dfs
    - build graph, graph <vertex, list<neighborr>> , a-> b, b depends on a?
    - dfs建图需要倒着建图，是因为打印的问题

*/

class Solution {
    private boolean isCycle = false;
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // sanity check

        // initial & build graph
        List<Integer> result = new ArrayList<>();
        int[] inDegree = new int[numCourses];
        Map<Integer, Set<Integer>> graph = buildGraph(numCourses, prerequisites, inDegree);


        // dfs& bfs
        Set<Integer> visited = new HashSet<>();
        Set<Integer> visiting = new HashSet<>();
        for (int i = 0; i < numCourses; i++) {
            dfs(graph, visited, visiting, result, i);
        }
        // bfs(graph, result, numCourses, inDegree);

        // is cycle?
        if (isCycle == true) {
            return new int[]{};
        }
        // return value
        int[] ret = new int[numCourses];
        for (int i = 0; i < result.size(); i++) {
            ret[result.size()- i -1] = result.get(i); // for dfs
            // ret[i] = result.get(i); // for bfs
        }
        return ret;

    }
    private void bfs(Map<Integer, Set<Integer>> graph, List<Integer> result, int numCourses, int[] inDegree){
        Deque<Integer> queue = new ArrayDeque<>();
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
            }
        }
        int count = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Integer cur = queue.poll();
                result.add(cur);
                count++;
                for (Integer nei: graph.getOrDefault(cur, new HashSet<>())) {
                    inDegree[nei]--;
                    if (inDegree[nei] == 0) {
                        queue.offer(nei);
                    }

                }

            }
        }
        if (count != numCourses) {
            isCycle = true;
        }
    }
    private void dfs(Map<Integer, Set<Integer>> graph, Set<Integer> visited, Set<Integer> visiting, List<Integer> result, int vertex){
        if (visiting.contains(vertex)) {
            isCycle = true;
            return;
        }
        if (visited.contains(vertex)) {
            return;
        }
        visiting.add(vertex);
        for (Integer nei: graph.get(vertex)) {
            dfs(graph, visited, visiting, result, nei);
        }
        visiting.remove(vertex);
        visited.add(vertex);
        result.add(vertex);
    }
    private Map<Integer, Set<Integer>> buildGraph(int numCourse, int[][] prerequisites, int[] inDegree) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < numCourse; i++) {
            graph.putIfAbsent(i , new HashSet<>());
        }
        for (int[] pre: prerequisites) {
            int first = pre[1];
            int second = pre[0];
            graph.get(first).add(second);  // pre[0] 是后修课，pre[1]是先修课
            inDegree[second]++;
        }
        return graph;
    }
}
```
````





More interesting implement could be seen in previous 基本功和母体
