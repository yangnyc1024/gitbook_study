# Question 0 Design Heap

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
  * compare the element with its parent
  * move it up when necessary.&#x20;
  * do this until the element does not to be moved
* PercolatedDown()
  * compare the element with its two children,&#x20;
  * if the smallest/largest one of the two children is smaller/larger than the element, swap the element with that child.&#x20;
  * do this until the element does not need to be moved.
* Offer()
  * 先把value 放到最后一个（complete tree的性质）
  * 再进行PercolateUp()（堆序性）
* Poll()
  * 先把最后一个value填补到第一个value
  * 再进行PercolateDown
* Heapify()
  * 把一个unsorted collection，具体变成一个Heap, O(n)

#### 详细说heapify()

* 把一个unsorted collection具体变成一个heap, O(n)

<mark style="color:blue;">Method 1: 对所有元素进行PercolateDown()</mark>

* <mark style="color:orange;">顺序，必须是从下往下对每个元素做percolateDown</mark> （因为你做percolateDown的时候，只能改变这一个元素，所以在从下往上的时候，后面的都做完了，所以ok）
* i.e.Pdown正确性，必须保证在PDown的时候西下方的元素已经满足堆序性



<mark style="color:blue;">Method 2: 对所有元素进行PercolateUp()</mark>

* 顺序，必须是从上往下对每个元素做percolateUp



<mark style="color:blue;">Question到底选哪个呢？</mark>

* PercolateDown() ---> O(n)
  * 可以用数学公式计算
  * 但是也可以看看，pDown不参与的元素是最后一层，i.e.参与的是 < n/2
* PercolateUp() ---> O(nlogn)
  * 可以用数学公式算
  * 但是也可以看看，pUp不参与的元素是第一个，i.e.参与的是n-1个(tree最后一层> half)
* 所以要用percolateDown





