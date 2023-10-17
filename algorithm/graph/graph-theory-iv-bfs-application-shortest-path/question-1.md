# Question 1











### Method 4 Bi-Directional BFS

```java
class BFSIterator {
    // 功能： next() hasNext()
    private Deque<Node> queue;
    private Map<Node, Integer> visited; // 每个点，从起点出发到这个点的最短路径
    
    public BFSIterator(Node init) {
        this.queue = new LinkedList<>();
        this.visited = new HashMap<>();
        queue.offer(init);
        visited.put(init, 0);
    }

}
```



```java
poblic int biDirectionalBFS(Node start, Node end) {
    BFSIterator bfsFromStart = new BFSIterator(start);
    BFSIterator bfsFromEnd = new BFSIterator(end);
    
    while (bfsFromSTart.hasNext() && bfsFromEnd.hasNext()) {
        int startSideMakeMove = bfsFromStart.next(bfsFromEnd);
        if (startSideMakeMove != NOT_MET_IN_THISROUND) {
            return startSideMakeMove;
        }
        int endSideMakeMove = bfsFromStart.next(bfsFromStart);
        if (endSideMakeMove != NOT_MET_IN_THISROUND) {
            return endSideMakeMove;
        }
    }
    return NOT_MET_IN_THISROUND;
}
```
