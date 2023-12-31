# Dijkstra Algorithm基本过程与理解

## Series S2: 求一点出发到一点/其他所有点的最短路径

* 使用条件：边上的权证可以有且不相同但必须为正值
* Series S1:讲了五个series（见前面的shortest path）





## **Use Case 1:求出一个点到一个点的最短路径**



**什么是Dijkstra Algorithm? Best First Search VS Dijkstra**

* Dijkstra：需要有一个Starting Node（题目给的），<mark style="color:purple;">每一次从到目前为止Cost最低的点出发（Expand）</mark>，generate所有它的邻居，直到我们Expand到targetNode/所有Node为止！
* <mark style="color:blue;">**每当一个点被Expand的时候，它的最短路径（从start到他）就确定了**</mark>



注意expand& generate

* expand表示你接下来要访问的
  * 所以你一旦访问了，就表示确定了，所以对于dijkstra来说，每次要访问的(expand)，一旦他被访问了，从源头点到该点的最短就确定了
  * 如果记录的每点cost最小，也就是costMark(x) = min Cost(源头，x)
    * min cost（源头，x）= minCost （源头，y） + minCost（y，x）
    * 这个成立的唯一条件，就是cost是正的\&cost函数是monotonicity increasing的？
* generate表示你potential需要访问的点

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
    Map<String, Integer> nodeToIndex = new HashSet<>(); //这个Map可以不要，根据你的构图决定
    int index = 0;
    for (String node: graph.keySet()) {
        nodeToIndex.put(node, index++);
    }
    int n = graph.size(); //有几个node
    int[] distances = new int[n]; //这个是记录node的对应的distance //有点像dp
    Arrays.fill(distances, Integer.MAX_VALUE); //现在把distance全部记录最大 
    boolean[] visited = new boolean[];    
    distance[nodeToIndex.get(start)] = 0;
    
    //至多node轮
    for (int i = 0; i < n - 1; i++) { //明确告诉你Dijkstra最多有多少轮
        int uIndex = selectMinimumIndex(distances, visited); // 从当前cost最低点出发// 这部分可以被pq优化
        visited[uIndex] = true; // u 是个index不是这个点,所以你要反向找回那个node
        for (GraphNode v: graph.getOrDefault(indexToNode(uIndex, nodeToIndex), new ArrayList<>())) {
            int vIndex = nodeToIndex.get(v.node);
            if (!visited[vIndex] && distances[uIndex] != Integer.MAX_VALUE && distances[uIndex] + v.weight < distance[vIndex]) {
                distances[vIndex] = distance[uIndex] + v.weight;
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
            minIndex = i;
        }
    }
    return minIndex;
}
```

这个array版本的实现

* 缺点：时间肯定不如现代版本的heap/treeMap/treeSet版本实现
* 优点：元和可读性以及区分性: already\_expanded & already\_generated
  * if (distances\[uIndex] + v.weight < distances\[vIndex]) {distances\[vIndex] = distance\[uIndex] +v.weight};
  * 在这个视线里面，如果一个点被generate多次，不管后面的generate比前面generate得到的结果好还是坏
  * distances\[i]只要visited是false i的状态都是already\_generated but not yet expand。存储的只会是最优解，一旦visited\[i] mark成为true了，说明被expanded





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
    Map<String, Integer> shortestPath = new HashMap<>(); //这个其实是你mark Visited，这里把mark和map合起来了嘛。。
    
    minHeap.offer(new GraphNode(Sstart, 0));
    
    while (!minHeap.isEmpty()) {
        GraphNode currentNode = minHeap.poll();
        String currentLabel = currentNode.label;
        int currentCost = currentNode.cost;
        // 第一次exapnd到target就可以结束了，上面的实现没有加
        if(currentLabel.equals(end)) {
            return currentCost;
        }
        // 已经expand过的点不再expand
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
            其实可以完全分开
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

* 不行，但是可以进行如下操作
* 优化Java PQ: Search + update: 除非自己实现PriorityQueue, MappedPriorityQueue
* 选择TreeSet/ TreeMap update: remove + insert

TC\&SC

* TC:普通的遍历算法O(|V| + |E|) ==> O((|V| +|E|) \* log |E|)
  * Dijkstra: O(|V+E| \* log(E))
  * 除非你做了generation的优化，我保证了每个点至多被generate一次O((V+E)log(V))
* SC: O(E) or O(V) if you optimize for generation



## **Use Case 2: 求出从一个点到所有点的最短路径**

shortestPaths 里其实存的就是每一个点的最短路径值，而我们只要把遇到target node就return的这个限制条件去掉就好

## **Use Case 3: Dijkstra在面试中的难点: Multiple-Dimension Node**

#### Example

* 告诉你地图中所有城市的道路，求从一个start城市出发，走exactly K步能哦租到的所有城市中，总距离和距离当前城市最近的城市
* graph representation？明白什么是点，什么是边，每个点能去哪些点
  * 为什么不用这个edge不好用，因为没法快速的知道，每个点能去哪些点
  * 比较好的表达方式 adjacency list
    * Map\<Node, Map\<Node, Integer>> weightGraph
    * Map\<Node, List\<Node>> unidirectedGraph



#### 小心

* 走exactly K步能得到的距离和最小 不等与
* first time走k步的city，因为可能还有些点没有看到
* K步之内的距离和最小，因为这里说的是我要走K步呀
* 思考：说白了，因为dijkstra解决的是，<mark style="color:red;">某个点，到某个点的最短路径，但是这里的问题没有给出到底到哪个点的？——》所以你就都看step = K——》让每次expand出来的点的step是排好序的</mark>

#### 多维度问题的关系

* 如果你保证，Expand点或者generate点的顺序是单调的，就可以在第一次遇到它就终止算法
* 如果你能保证你generate点的时候，从小到达的单调递增的来generate，甚至可以在generate mark visited
* 如果你能保证你expand点的顺序是单调的，那就可以在第一次expand到他的时候终止





#### Summary

* Dijkstra算法中每exapnd一次，就确定了从点A到点B的最短路径，往后只能增大不能减少！如果求的是从一个点到所有点的最短路径，也只需要做一次！One to ALL！
* 是否可以在Generate的时候Mark Visited：不一定
* 时空复杂度: O(|V| +|E|) log(|E|)
  * 每个点允许被generate多次但是最多只能被expand一次
  * 如果我们自己实现MappedPriorityQueue，那么可以实现Node只能被Generated一次，但是非常复杂情况不如用TreeMap/TreeSet代替更为简洁
* MappedPriortyQueue：Use case是我们遇到一个已经generated的点的时候，Map找到Node Position，UpdatedValue +上下调整
