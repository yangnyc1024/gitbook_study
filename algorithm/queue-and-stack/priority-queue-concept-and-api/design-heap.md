# Design Heap

## 重点（保持堆序性+ complete tree）

#### 堆序性

* maxHeap: 对于每个subtree最大值总在顶端
* minHeap：对于每个subtree最小值总在顶端

#### complete tree

* heap is actually a complete binary tree
* 除了最后一层，上面全满
* null还得出现在右边

#### array-based binary tree?

* O(1) 的时间，你给我们一个index i
  * i's left child index = 2\* i + 1
  * i's right child index = 2\* i + 2
  * i's parent  = (i -1)/2

####   常用API

* PercolateUp()
  * &#x20;compare the element with its parent, move it up when neccessary. do this until the element does not to be moved
* PercolatedDown()
  * compare the lement with its two chidren, if the smallest one of the two children is smaller than the element, swap the element with that child. do this until the elment does not need to be moved.
* Offer()
  * 先把value 放到最后一个，再进行PercolateUp()
* Poll()
  * 先把最后一个value填补到第一个value再进心PercolateDown
* Heapify()
  * 把一个unsorted collection，具体变成一个Heap, O(n)

