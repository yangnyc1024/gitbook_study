# Question 1 Maximum Cost of Trip With K Highways

```java
class Node {
    String city;
    int cost;
    int steps;
    public Node(String city, int cost, int steps) {
        this.city = city;
        this.cost = cost;
        this.steps = steps;
    }
    // HashCode, Equals
    // Steps + Costs 一样的，才是一样的点
}
public String getCityWithMinCostInkSteps(String startCity, int k, Map<String, List<Node> graph>) {
    PriorityQueue<Node> minHeap = new PriorityQueue<>((a,b) -> Integer.compare(a.cost, b.cost));
    int minCost = -1;
    
    pq.offer(new Node(startCity, 0, 0));
    Set<Node> visited = new HashSet<>();
    
    while (!minHeap.isEmpty()) {
        Node currentNode = minHeap.poll();
        String currentCity = currentNode.city;
        int currentCost = currentNode.cost;
        int currentSteps = currentNode.steos;
        if (currentStep == k) {
            return currentCost;
        }
        if (visited.contains(currentNode)) continues;
        visited.add(currentNode);
        Lis<Node> neighbors  = graph.getOrDefault(currentCity, new ArrayList<>());
        for (Node neighbor: neighbors) {
            minHeap.offer(new Node(neighbor.city, currentCost + neighbor.cost, currentSteps + 1 ));
        }
    }
    return minCost;
}
```



#### 多维度的一个值得思考的问题

第一次expand到K= targetStep的点，是不是从起始出发点出发走Exactly K步能到达的点distance sum最小的点（假设所有的edge cost都是严格大于0）

* 假设：第一次expand到K = targetStep的点不是所有exactly K步到的点中最小的点，也就是说存在某一个点，将来会被expand出来，step等于k且cost <当前cost
* proof在这次expand之前，minHeap中会存在
  * CNODE(Step = k, CurrentCost = X, name)
  * OtherNode1(Step = K, CurrentCost = X, name)
  * OtherNode2(Step = K, CurrentCost = X, name)
  * OtherNode3(Step = K, CurrentCost = X, name) 不可能存在，矛盾了，也会被expand出来
  * OtherNode4(Step < K, CurrentCost < X, name) 不可能存在，矛盾了，也会被expand出来
  * OtherNode5(Step < K, CurrentCost = X, name)
  * OtherNode6(Step < K, CurrentCost =>X, name)
* 分析
  * 由Type 1产生的点和现在的解一样优秀: otherNode1 Step = K, Cost = currentCost!
  * 由Type 2产生的点一定不比现在的解更好：otherNode2 Step = K, Cost > currentCost ! distnace sum一定会更大
  * 由Type 5产生的点一定不比现在的解更好：
    * ohterNode5 Step < K Cost = currentCost 为了让step = K还得多走几步
    * final cost = 现在的cost + 后面多走的cost = X + moreCost. > X
  * 由Type6产生的点不一定比现在的解更好：现在还没走到k步呢都已经打了，边又是正的，就更大了
* 所以假设错误
  * 也就是不存在某一个点，将来会被expand出来，step = K且 cost< currentCost
* 所以第一次expand到K=targetStep的点，一定是所有exactly K步到达的点中最小的
