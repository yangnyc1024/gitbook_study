---
description: Question 1
---

# Question 1

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
