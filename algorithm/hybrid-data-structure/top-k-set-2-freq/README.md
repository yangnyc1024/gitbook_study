# Advance 3: Top K set 2 freq

## Summary

此类问题最需要什么？

1. lookUp操作（排序property到element）
2. arbitrary access element（update/insert/delete）
3. 同时整个set还是个sorted element基于该property(access, freq, etc)

所以思考逻辑如下，

1. 对于第一个，因为你要update from value to freq（排序property）
   * 因为value是没有什么sorted，所以会想到需要Map\<value, freq>(为了安全你就使用Map\<value, element>)
2. 对于第二&三个，property为了可以拿到top K，你需要一个结构可以给你最大最小
   * 想到了<mark style="color:blue;">部分sorted</mark>，很自然想到treeSet\<freq>(为了安全你就使用<mark style="color:blue;">treeSet\<element></mark>)
     * 这里如果没有arbitrary delete/update，可以用<mark style="color:orange;">priorityQueue</mark>
   * 同时可能用<mark style="color:blue;">全部sorted</mark>，如果是某个顺序add（就是只add尾部）
     * 所以第一反应应该是<mark style="color:orange;">bucket list(based on value)</mark>
     * 所以就用<mark style="color:blue;">doubleLinkedList\<element></mark>











Top K frequent Elements

LRU

LFU

Cache
