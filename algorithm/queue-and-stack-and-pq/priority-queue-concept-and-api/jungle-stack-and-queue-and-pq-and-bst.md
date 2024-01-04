# Deep Dive

| 数据结构（逻辑层）           | 内存里的存放方法             | 对应的java class            | 对应的java interface |
| ------------------- | -------------------- | ------------------------ | ----------------- |
| queue(FIFO)         | array/ linked list   | ArrayDeque / LinkedList  | Queue             |
| stack(LIFO)         | array / linked list  | ArrayDeque / LinkedList  | Deque             |
| deque(double-ended) | array/ linked list   | ArrayDeque / LinkedList  | Deque             |
| heap                | array(abstract tree) | PriortyQueue             | Queue             |

* The PriorityQueue is implemented using an array.(Array-based Complete Tree)
*   What is MinHeap vs MaxHeap?

    * &#x20;堆顶元素是最大/小值，并且每个subtree root均是该子树最大/小值


* 判断heap(complete tree+ 堆序性)
  * 堆序性：堆永远可以保证每个子树的最值在顶端
    * 类似BBST中的平衡性，不管做了任何操作，总能维持自己是个最大/最小堆的性质



## Heap API



* 该用的是最大最小，但是查找（删除）就不太给力

## Heap vs Self-balancing BST

|                    | search(Object) | delete() mark | remove(Object): search + delete |
| ------------------ | -------------- | ------------- | ------------------------------- |
| heap               | O(n)           | O(log n)      | O(n + log n) = O(n)             |
| self-balancing BST | O(log n)       | O(log n)      | O(log n)                        |

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-17 at 1.47.27 PM.png" alt=""><figcaption></figcaption></figure>

