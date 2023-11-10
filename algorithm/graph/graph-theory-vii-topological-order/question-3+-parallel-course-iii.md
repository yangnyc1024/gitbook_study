---
description: https://leetcode.com/problems/parallel-courses-iii
---

# Question 3+ Parallel Course III

code has some problems

````java
// Some code

```java
class Solution {
    public int minimumTime(int n, int[][] relations, int[] time) {
        // sanity check
        // initial result & graph & visitedCheck&& indegree 
        int[] result = new int[1];
        int[] indegree = new int[n];
        int[] totalCourseCheck = new int[1];
        // build graph 

        List<List<Integer>> graph = buildGraph(relations, n, indegree);

        // bfs
        bfs(graph, indegree, n, result, time, totalCourseCheck);

        // check if it is circle
        if (totalCourseCheck[0] != n) {
            return -1;
        }
        // return
        return result[0];
    }
    private void bfs(List<List<Integer>> graph, int[] indegree, int n, int[] result, int[] time, int[] totalCourseCheck) {
        Queue<Integer> queue = new ArrayDeque<>();
        initialState(queue, indegree, time, result, n);
        while (!queue.isEmpty()) {
            int curResult = 0;
            int size = queue.size();
            for (int i = 0 ; i < size; i++)  {
                int curCourse = queue.poll();
                totalCourseCheck[0] ++;
                curResult = Math.max(curResult, time[curCourse]);
                for (Integer nei: graph.get(curCourse)) {
                    indegree[nei]--;
                    if (indegree[nei] == 0) {
                        // curResult = Math.max(curResult, time[curCourse]);
                        queue.offer(nei);
                    }
                }
            }
            result[0] += curResult;
        }

    }
    private void initialState(Queue<Integer> queue, int[] indegree, int[] time, int[] result, int n)  {
        int curResult = 0;
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                // curResult = Math.max(curResult, time[i]);
                queue.offer(i);
            }
        }
        // result[0] += curResult;
    }
    private List<List<Integer>> buildGraph(int[][] relations, int n, int[] indegree) {
        List<List<Integer>> graph  = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add (new ArrayList<>());
        }
        for (int[] relation : relations) {
        // for example, relation[1], relation[1][0] -- >relation [1][1]
            int first = relation[0] - 1;
            int second = relation[1] - 1;
            indegree[second]++;
            graph.get(first).add(second);
        }
        return graph;
    }
}

// how to calculate time? each round, currentLevel = Math.max(currentLevel, this time(which is indegree = 0))
```
````
