---
description: Question
---

# Question 2 Keys and Rooms

Step 1: 分析问题

* this is a graph problem
* vertical: room
* edge: the key from the current room

Step 2: 声明是图中间什么问题

* reachable problem in the graph

Step 3: method: dfs + bfs



图论中，题目提到1，n: there are n rooms(nodes) labeled from 0 to n-1 ==> please use an array to mark visited or other



```java
public boolean canVisitedAllRooms(List<List<Integer>> rooms) {
    Set<Integer> visited = new HashSet<>();
    int totalNumberOfRoomsNeedsToVisit = rooms.size();
    dfs(rooms, 0, visited); //一定要注意图不一定是联通的
    bfs(rooms, 0, visited);
    return visited.size() == totalNumberOfRoomsNeedsToVisit;
}
private dfs(List<List<Integer>> rooms, int current, Set<Integer> visited) {
    if (visited.contains(current)) {
        return;
    }
    visited.add(current);
    List<Integer> neis = rooms.get(current);
    if (!neis.isEmpty()) {
        for (Integer nei: neis) {
            dfs(rooms, nei, visited);
        }
    }
}
private void bfs(List<List<Integer>> rooms, int current, Set<Integer> visited) {
    Deque<Integer> queue = new ArrayDeque<>();
    queue.offer(current);
    visited.add(current);
    while (!queue.isEmpty()) {
        int cur = queue.poll();
        List<Integer> neis = rooms.get(cur);
        if (!neis.isEmpty()) {
            for (Integer nei: neis) {
                if (!visited.contains(nei)) {
                    queue.offer(nei);
                    visited.add(nei);
                }
            }
        }
    }
}
```

