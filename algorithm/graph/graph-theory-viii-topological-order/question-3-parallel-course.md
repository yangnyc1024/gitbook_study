# Question 3 Parallel Course



题目问我们最少需要几个学期去上课：

* 为什么不把课都一个学期上，因为你和你的前置课程不能在同一学习

所以怎么上课最快？所以怎么上课最慢？

* 同样优先级的可一定要一个学期上就比较快
* 最慢怎么上？明明可以一起上的课，一个一个来chain

这题本质是对拓扑图的按层遍历

```java
public int minimumSemesters(int n, int[][] relations) {
    Map<Integer, List<Integer>> graph = new HashMap<>();
    int[] inDegree = new int[n + 1];
    /*
        relations[i] = [preCourse, nextCourse]
        relation[i][0] first relations[i][1] second relation
        relaiton[i][0] --> relation[i][1] index 0 里面加1，1的入度++
    */ 
    for (int[] relation: relations) {
        inDegree[relation[1]]++;
        graph.putIfAbsent(relation[0], new ArrayList<>());
        graph.get(relation[0]).add(relation[1]);
    }
    
    Deque<Integer> queue = new ArrayDeque<>();
    // step 1: generate all indegree 0 nodes
    for (int i = 1; i <= n; i++) {
        if (inDegree[i] == 0) {
            queue.offer(i);
        }
    }
    int semester = 0;
    int count = 0;
    
    // step 2: BFS topological process
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            Integer cur = queue.poll();
            count++;
            for (Integer nei: graph.getOrDefault(cur, new ArrayList<>())) {
                inDegree[nei]--;
                if (inDegree[nei] == 0) {
                    queue.offer(nei);
                }
            }
        }
        semester++;
    }
    if (count != n) {
        return -1;
    }
    return semester;
}
```

















































































































