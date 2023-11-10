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
public List<List<Integer>> findOrder(int numCourses, int[][] prerequisites) {
        // sanity check
        if (numCourses < 0) return new;
        if (prerequisites == null || prerequisites.length == 0 || prerequisites[0].length  == 0) {
            return false;
        } 

        // buildGraph
        int[] inDegree = new int[numCourses];
        List<List<Integer>> graph = buildGraph(numCourses, prerequisites, inDegree);
        List<Integer> topoSortREsult = new ArrayList<>();

        // initalQueue with all indegree = 0 
        Deque<Integer> queue = new ArrayDeque<>();
        for (int i = 0; i < numCourses;  i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
            }
        }

        // bfs
        int count = 0;
        while (!queue.isEmpty()) {
            Integer cur = queue.poll();
            topoSortResult.add(cur);
            count++;
            for (Integer nei: graph.getOrDefault(cur, new ArrayList<>())) {
                inDegree[nei]--;
                if (inDegree[nei] == 0) {
                    queue.offer(nei);
                }

            }

        }

        // check if circle, i.e. finish
        if (count != numCourses) {
            return new ArrayList<>();
        }
        return topoSortResult;
    }
    private List<List<Integer>> buildGraph(int numCourses, int[][] prerequisites, int[] inDegree) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            graph.add(new ArrayList<>());
        }
        /*
            [1, 0], 0 -> 1
        */
        for (int[] prerequisite: prerequisites) {
            int first = prerequisite[1];
            int second = prerequisite[0];
            inDegree[second]++;
            graph.get(first).add(second);
        }
        return graph;
    }
```
````





More interesting implement could be seen in previous 基本功和母体
