---
description: >-
  https://leetcode.com/problems/maximum-cost-of-trip-with-k-highways/description/
---

# Question 2: Maximum Cost of Trip With K HighWays

#### 思考

* Shortest Path Problem ==> Optimization on the cost of path problem
* 和我们讨论的母题的区别：可以从任意点出发

#### High Level

* graph problem, what graph?
  * graph --> 点的定义，cost 代表什么物理意义--> cost是否为正数

#### Middle Level(Dijkstra细节)

* expand? generation?
* 终止条件？
* 怎么去重复？
* 多维度，如果你能保证，expand点和generate点的顺序是单调，就可以第一次遇到它就终止算法
  * 如果你能保证你generate点的时候，从小到大的单调递增的来generate，甚至可以在generate mark visited
  * 如果你保证你exapdn点的顺序是单调的，那就可以在第一次expand到他的时候终止



````java
`
class Solution {
    class Node {
        int id;
        int cost;
        int step;
        public Node(int id, int cost, int step) {
            this.id = id;
            this.cost = cost;
            this.step = step;
        }
    }
    public int maximumCost(int n, int[][] highways, int k) {
        // build grpah

        Map<Integer, List<int[]>> graph = buildGraph(highways);
        // dijsktra

        int max = -1;
        for (int i = 0; i < n; i++) {
            boolean[] visited = new boolean[n];
            PriorityQueue<Node> maxHeap = new PriorityQueue<>((a, b) -> Integer.compare(b.cost, a.cost));
            int curMax = dijsktra(i, graph, maxHeap, visited, k);
            max = Math.max(curMax, max);
        }
        return max;
    }
    private int dijsktra(int i , Map<Integer, List<int[]>> graph, PriorityQueue<Node> maxHeap, boolean[] visited, int totalStep) {
        int max = -1;
        maxHeap.offer(new Node(i, 0, 0));
        while (!maxHeap.isEmpty()) {
            Node cur = maxHeap.poll();
            visited[cur.id] = true;
            if (cur.step == totalStep) {
                max = Math.max(max, cur.cost);
                break;
            }
            List<int[]> neighbors = graph.get(cur.id);
            if (neighbors == null) continue; /// 这个别忘了
            for (int[] nei: neighbors) {
                if (!visited[nei[0]]) {
                    maxHeap.offer(new Node(nei[0], cur.cost + nei[1], cur.step + 1));
                }
            }
        }
        return max;
    }
    private Map<Integer, List<int[]>> buildGraph(int[][] highways) {
        Map<Integer, List<int[]>> graph = new HashMap<>();
        for (int i = 0; i < highways.length; i++) {
            int u = highways[i][0];
            int v = highways[i][1];
            int fee = highways[i][2];
            graph.putIfAbsent(u, new ArrayList<>());
            graph.putIfAbsent(v, new ArrayList<>());
            graph.get(u).add(new int[]{v, fee});
            graph.get(v).add(new int[]{u, fee});

        }
        return graph;
    }
}
```
````

