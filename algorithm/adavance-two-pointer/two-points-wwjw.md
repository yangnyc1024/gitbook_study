# Two Points WWJW

#### Apply on sequence type data

* array
* &#x20;linked list
* stream
* &#x20;sequenced view of other data

#### Categories? (X sum, partition, removal, deduplication, sliding window)

* 相向
  * rainbow sort/ quick sort/ quick select (partition)
  * move all 0s to the right end, no need to maintain relative order
  * 2 sum, 3 sum 以及各种变种
* 同向
  * deduplication 1，2，3，4
  * rainbow sort/ quick sort/ quick select (partition)
  * removal(maintain relative order)
  * move all 0s to the right end, maintain relative order
  * sliding window relevant
    * longest substring with at most 2 distict characters
    * strstr( robin karp)

#### 理解

* 这个题目用的是什么2 pointer strategy？
* 为什么可以用2 pointer strategy？
* 扩展一下，什么样的题目可以用2 pointer strategy？







核心点是

1）这两个点的方向？

2）固定一个点后，剩下一个点移动的位置

