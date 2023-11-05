# Question 3 Kth Smallest with Only 3, 5, 7 As Factors

#### Question?

* (x,y,z)

#### High Level

* graph problem: undirect graph
  * vertex: (x,y,z)
  * edge: only one different from (x,y,z)
* method:Dijkstra method(bfs)
  * k-1 step more to find the kth smallest(本质问题就是从（1，1，1）走k步能到的点)

#### Middle Level

* initial state: (1,1,1)
* expand:第几次expand出现的就是matrix里第几小的元素
* generate：x，y，z possible + 1
* termination condition： k step
* deduplication
  * 因为Generation的顺序是一样的（因为你从3开始嘛），同样X,Y,Z带来的cost一定相同---> mark visited at generation

#### TC& SC

* O(klog 2k)--> O(klog K)
* space: O(2k)--> O(k)\[O(3k--> k) for set, O(2k--> k) for priorityQueue]









```java
public long kth(int k) {
    PriorityQueue<Long> minHeap = new PriorityQueue<>();
    Long start = 3* 5* 7L;
    Set<Long> visited = new HashSet<>();
    minHeap.offer(start);
    visited.add(start);
    int step = 1;
    while (!minHeap.isEmpty()) {
        Long curValue = minHeap.poll();
        if (step == k) {
            return curValue;
        }
        if (!visited.contains(curValue * 3)) {
            minHeap.offer(curValue * 3);
            visited.add(curValue * 3);
        }
        if (!visited.contains(curValue * 5)) {
            minHeap.offer(curValue * 5);
            visited.add(curValue * 5);
        }
        if (!visited.contains(curValue * 7)) {
            minHeap.offer(curValue * 7);
            visited.add(curValue * 7);
        }
        step++;
    }
    return -1;
}
```

