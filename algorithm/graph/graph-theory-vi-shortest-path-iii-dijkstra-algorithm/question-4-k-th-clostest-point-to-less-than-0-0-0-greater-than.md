# Question 4 K th Clostest Point to <0,0,0>



#### High Level

* Graph?&#x20;
  * vertex:(x,y,z)
  * edge: x,y,z +1&#x20;
  * graph representation:
    *
* method:
  * bfs-2

Middle Level

* using priorityQueue
* inital state: (0,0,0)
* expand:第几次expand出现的就是matrix里第几小的元素
* generate: x,y, z  choose one to plus 1
* termination condition: when the k-th element is about to be expanded
* deduplication: 不去同样的x,y,z





```java
class Solution{
    class Node {
        int x;
        int y;
        int z;
        double cost;
        public Node(int x, int y, int z, double cost) {
            this.x = x;
            this.y = y;
            this.z = z;
            this.cost = cost;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj) {
                return true;
            }
            if (!obj instanceof Node) {
                return false;
            }
            Node that = (Node)obj;
            return that.x == this.x && that.y == this.y && that.z = this.z;
        }
        @Override
        public int hashCode() {
            return this.x* 31 + this.y *31* 31 + this.z *31 *31 *31;
        }
    }
    public List<Integer> closest(int[] a, int[] b, int[] c, int k) {
        List<Integer> result = new ArrayList<>();
        PrirotyQueue<Node> minHeap = new PriortyQueue<>(k, new Comparator<Node>(){
            @Override
            public int compare(Node c1, Node c2) {
                if (c1.cost == c2.cost) {
                    return 0;
                }
                return c1.cost < c2.cost ? -1. 1;
            }
        });
        double startCost = getEuclideanDistance(a,b,c,0,0,0);
        Node start = new Node(0,0,0, startCost);
        Set<Node> visited = new HashSet<>();
        minHeap.offer(start);
        visited.add(start);
        int step = 1;
        while (!minHeap.isEmpty()) {
            Node curNode = minHeap.poll();
            if (step == k) {
                result.add(a[curNode.x]);
                result.add(b[curNode.y]);
                result.add(c[curNode.z]);
                return result;
            }
            if (curNode.x + 1 < a.length) {
                double newDistance1 = getEuclideanDistance(a,b,c, curNode.x + 1, curNode.y, cuuNode.z);
                Node newNode1 = new Node(curnode.x + 1, curNode.y, curNode.z, newDistance1);
                if (!visited.contains(newNode1)){
                    minHeap.offer(newNode1);
                    visited.add(newNode1);
                }
            }
            if (curNode.y + 1 < b.length) {
                double newDistance2 = getEuclideanDistance(a,b,c, curNode.x, curNode.y + 1, cuuNode.z);
                Node newNode2 = new Node(curnode.x + 1, curNode.y, curNode.z, newDistance1);
                if (!visited.contains(newNode2)){
                    minHeap.offer(newNode2);
                    visited.add(newNode2);
                }
            }
            if (curNode.x + 3 < a.length) {
                double newDistance1 = getEuclideanDistance(a,b,c, curNode.x, curNode.y, cuuNode.z + 1);
                Node newNode3 = new Node(curnode.x, curNode.y, curNode.z + 1, newDistance1);
                if (!visited.contains(newNode3)){
                    minHeap.offer(newNode3);
                    visited.add(newNode3);
                }
            }
            step++;
        }
        return result;
    }    
    private double getEucldeanDistance(int[] a, int[] b, int[] c, int x, int y, int z) {
        return Math.sqrt(a[x] * a[x] + b[y] * b[y] + c[z] * c[z]);
    }    
}
```

