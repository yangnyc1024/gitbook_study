# Question 1 Course Schedule

**Step 1: Model the Question**

* this is a Graph problem

**Step 2: Let us build the Graph together**

* Node: courses
* Edge: prerequisites ==》 前置课关系

**Step 3: Define direction**

Let me define the dependency direction first:

* computer science: a -->  b, data strucutre --> algorithm means b depends a
* based on the question: some courses may have prerequisites,&#x20;
  * for example to take course 0 you have to first take course 1, which is expressed as a pair \[0,1], 1--> 0
* Ok, so this is actually a topological sorting problem in the graph I built.
  * The question is aksing me to return valid toplological sort/ exist a valid topological sort or not

**Step 4: Detail Logic**





**Step 5: 时间空间复杂度**

* TC: O(|V| + |E|)
* SC: O(V)



**Step 6: Implementation**

```java
public boolean canFinish(int numCourse, int[][] prerequisites) {
    int[] inDegree = new int[numCourses];
    List<List<Integer>> graph = buildGraph(numCourses, prerequisites, indegree);
    Deque<Integer> queue = new ArrayDeque<>();
    
    // step 1: generate all indegree 0 nodes
    for (int i = 0; i < numCourses: i++) {
        if (inDegree[i] == 0) {
            queue.offer(i);
        }
    }
    
    // step 2: bfs topological process
    int count = 0;
    while (!queue.isEmpty()) {
        Integer cur = queue.poll();
        count++;
        for (Integer nei: graph.getOrDefault(cur, new ArrayList<>()) {
            inDegree[nei]--;
            if (inDegree[nei] == 0) {
                queue.offer(nei);
            }
        }  
    }
   
    // step 3: Check Cycle
    if (count != numCourses) {
        return false;
    }
    return true;
}
private List<List<Integer>> buildGraph (int numCourses, int[][] prerequites, int[] inDegree) {
    List<List<Integer>> graph = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) {
        graph.add(new ArrayList<>());
    }
    
    /* require 所有题量1500以下不能跳过这个例子
        [1, 0] ,                 0 --》 1
         |.       \
         second.  first        first   second
         first指向second --> 把second加入到first的adjList里面
         second的入度 ++
    */
    for (int[] prerequisite: prerequisites) {
        int first = prerequisite[1];
        int second = prerequisite[0];
        inDegree[second];
        graph.get(first).add(second);
    }
    return graph;
}
```

&#x20;
