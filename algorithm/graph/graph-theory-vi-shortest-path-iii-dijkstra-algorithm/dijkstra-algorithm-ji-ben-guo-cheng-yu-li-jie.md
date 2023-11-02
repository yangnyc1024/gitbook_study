# Dijkstra Algorithm基本过程与理解

## Series S2: 求一点出发到一点/其他所有点的最短路径

* 使用条件：边上的权证可以有且不相同但必须为正值
* Series S1:讲了五个series





## **Use Case 1:求出一个点到一个点的最短路径**



**什么是Dijkstra Algorithm? Best First Search VS Dijkstra**

* Dijkstra：需要有一个Starting Node（题目给的），<mark style="color:purple;">每一次从到目前为止Cost最低的点出发（Expand）</mark>，generate所有它的邻居，直到我们Expand到targetNode/所有Node为止！
* <mark style="color:blue;">**每当一个点被Expand的时候，它的最短路径（从start到他）就确定了**</mark>

**Greedy算法**

* 不看所有解，我觉得按着某一种方法（aha point）去走，我就得到最优解
* Greedy算法需要证明，也需要一些灵感！

**反证法：会不会有一个被expand的点，其实从源点到它的最短路径没有确定，会在后面的expansion来确定**

* 被Generate的点， A(13), B(15), D(17)
* Expansion： dis(Src, first\_time\_C) = 10
* dis(Src, second\_expanded\_C) = initial dis from src to the cur node(>= 10) + dis of all the path behind
* dis(Src, second\_expanded\_C) > dis(Src, first\_time\_C)
* 假设错误

**在Dijsktra算法中需要注意**

* 明确你的cost是什么
* 我们允许一个点被Generate多次，先generate的不一定是最短路径（时间最先！=cost最优）
* 在有权重图中，<mark style="color:orange;">Mark Visited at Generation是不一定正确的！！</mark>

<mark style="color:blue;">**Cost of Neighbor When Generation**</mark>

* <mark style="color:blue;">dis(src, nei)  = dis(src, cur) + weight of (cur, nei)</mark>



### **General Implementation for Dijkstra**

```java
class GraphNode{
    String node;
    int weight;
    public GraphNode(String node, int weight) {
        this.node;
        this.weight;
    }
}
public int findShortestPath(String start, String end, Map<String, List<GraphNode>> graph) {
    // mapping for node and index
    Map<String, Integer> nodeToIndex = new HashSet<>(); //这个Map可以不要，根据你的构图
    int index = 0;
    for (String node: graph.keySet()) {
        nodeToIndex.put(node, index++);
    }
    int n = graph.size();
    int[] distances = new int[n];
    Arrays.fill(distances, Integer.MAX_VALUE);
    boolean[] visited = new boolean[];    
    distance[nodeToIndex.get(start)] = 0;
    
    //至多node轮
    for (int i = 0; i < n -1; i++) { //明确告诉你Dijkstra最多有多少轮
        int u = selectMinimumIndex(distances, visited); // 从当前cost最低点出发
        visited[u] = true; // u 是个index不是这个点
        for (GraphNode v: graph.getOrDefault(indexToNode(u, nodeToIndex), new ArrayList<>())) {
            int vIndex = nodeToIndex.get(v.node);
            if (!visited[vIndex] && distances[u] != Integer.MAX_VALUE && distances[u] + v.weight < distance[vIndex]) {
                distances[vIndex] = distance[u] + v.weight;
            }
        }
    }
    return distances[nodeToIndex.get(end)];
}

private String indexToNode(int index, Map<String, Integer> nodeToIndex) {
    for (Map.Entry<String, Integer> entry: nodeToIndex.entrySet()) {
        if (entry.getValue().equals(index)) {
            return entry.getKey();
        }
    }
    return null;
}
private int seletecMinimumIndex(int[] distances, boolean[] visited) {
    int minIndex = -1;
    int minValue = Integer.MAX_VALUE;
    for (int i = 0; i < distance.length; i++) {
        if (!visited[i] && distances[i] < minValue) {
            minValue = distance[i];
            minIndex = 1;
        }
    }
    return minIndex;
}
```







### **General Implementation for Dijkstra 现代版**

```java
class GraphNode{
    String label;
    int cost;// 到目前为止的cost，src到这个node的距离和
    public GraphNode(String label, int cost) {
        this.label;
        this.cost;
    }
}
public int findShortestPath(String start, String end, Map<String, List<GraphNode>> graph) {
    if (start.equals(end)) return 0;
    PriorityQueue<GraphNode> minHeap = new PriorityQueue<> ((node1, node2) -> .compare(node1.cost, node2.cost));
    Map<String, Integer> shortestPath = new HashMap<>();
    
    minHeap.offer(new GraphNode(Sstart, 0));
    
    while (!minHeap.isEmpty()) {
        GraphNode currentNode = minHeap.poll();
        String currentLabel = currentNode.label;
        int currentCost = currentNode.cost;
        // 第一次exapnd到target就可以结束了，上面的实现没有加
        if(currentLabel.equals(end)) {
            return currentCost;
        }
        // 已经exapnd过的点不再expand
        if (shortestPath.containsKey(currentLabel)) {
            continue;
        }
        shortestPath.put(currentLabel, currentCost);
        
        for(GraphNode neighbor: graph.getOrDefualt(currentLabel, new ArrayList<>()) {
            String neighborLabel = neighbor.label;
            int totalCostToNeighbor = currentCost + neighbor.cost;
            // given graph 初始化cost储存的是weight
            
            if (!shortestPath.containsKey(neighborLabel)) {
                minHeap.offer(new GraphNode(neighborLabel, totalCostToNeighbor));
            }
            /*
            case 1: neighbor node 已经被expand过了
                无视
            case 2: neighbor node虽然没有被exapnd过， 被generate过了
                Map<Node, Integer> already_generateMap: <Node, 上一次generate的cost>
                如果这一次generate的totalCostToNeighbor比上一次低才generate
            case 3: 这个node还没有被generate过
                直接generate
            */
        }
        return -1;
}
```

Quesiton: 我能不能对于这种被generate的点，直接在PriorityQueue里更新的Entry？

* 优化JAva PQ: Search + update: 除非自己实现PriorityQueue, MappedPriorityQueue
* TreeSet/ TreeMap update: remove + insert

TC\&SC

* TC:普通的遍历算法O(|V| + |E|) ==> O((|V| +|E|) \* log |E|)
  * Dijkstra: O(|V+E| \* log(E))
  * 除非你做了generation的优化，我保证了每个点至多被generate一次O((V+E)log(V))
* SC: O(E) or O(V) if you optimize for generation



## **Use Case 2: 求出从一个点到所有点的最短路径**

shortestPaths 里其实存的就是每一个点的最短路径值，而我们只要把遇到target node就return的这个限制条件去掉就好

## **Use Case 3: Dijkstra在面试中的难点: Multiple-Dimension Node**
