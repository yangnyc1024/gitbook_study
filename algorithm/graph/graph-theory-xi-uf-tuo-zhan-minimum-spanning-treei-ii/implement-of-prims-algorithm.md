# Implement of Prim's Algorithm

## Implementation of Prim's Algorithm



### Method 1: 朴素法

getUsedInput() is a magic function that get user input for what we need!

```java
int N = getUserInput();
int[][] graph = getUserInput();
int[] dist = new int[N + 1];
int[] visited = new int[N + 1];



// 习惯是如果不存在就return INF, main函数里调用prim的时候要检查return得结果，是不是INF
public int prim() {
    Arrays.fill(dist, Integer.MAX_VALUE);
    int result = 0;
    
    for (int i = 0; i < N; i++) {
        //找出一个距离现在集合最近的点，这个是算法的核心部分，而不是找的是原点最近的点
        int target = -1;
        for (int j = 1; j <= N; j++) {
            if (!visited[j] && (target == -1 || dist[target] > dist[j])) {
                target= j;
            }
        }
        if (i != 0 && dist[target] == Integer.MAX_VALUE) {
            return Integer.MAX_VALUE;
        }
        // 默认是没有负环
        if (i != 0) {
            result += dist[target];
        }
        
        // 更新target加入以后，与target相邻neighbor到现有MST集合的最短距离
        for(int j = 1; j <= N; j++) {
            dist[j] = Math.min(dist[j], graph[target]);
            // VS dijkstra: dist[j] = Math.min(dist[j], dist[target] + graph[target][j])
            
        }
        visited[target] = true;
    }

    return result; // 注意如果有点不联通则不存在最小生成树
}
```





### Method 2: 堆化实现

```java

class Node {
    int id;
    int dist; // 刚才朴素法的距离：这个点
}

class Edge {
    int src;
    int dest;
    int weight;
}





// 习惯是如果不存在就return INF, main函数里调用prim的时候要检查return得结果，是不是INF
public List<Edge> primImp12(List<Edge>[] graph) {
    int v = graph.length;
    PriorityQueue<Node> minHeap = new PriorityQueue<>((a,b) => Integer.compare(a.dist, b.dist));
    
    
    int[] dist = new int[N + 1];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[0] = 0;
    
    boolean[] visited = new int[N + 1];
    minHeap.offer(new Node(0,0));
    List<Edge> result = new ArrayList<>();
    
    while (!minHeap.isEmpty()) {
        Node node = minHeap.poll();
        int u = node.id;
        
        visited[u] = truel
        for (Edge: edge: graph[u]) {
            int v = edge.dest;
            if (!visited[v] && edge.weight < dist[v]) {
                dist[v] = edge.weight;
                minHeap.offer(new Node(v,dist[v]));
                result.add(edge);
            }
        }
    }
    return result;       
}
```

