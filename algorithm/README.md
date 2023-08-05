# Summary

## Hybrid Data Structure&#x20;

* 如何表达这个hybrid data structure
  * 注意的是根据每个element(key, value, index)所要储存的data structure来变形
* data structure的细节
  * 不sorted (queue? )
    *
  * partial sorted(heap/ treeSet)
    * 可以帮助其中一个element找出最值
      * 需要的是map\<element, index>, container(element)
  * total sorted ((list/array, double-linkedlist))
    * linkedlist\<element>, map\<element, index>?

## Graph

* 如何表达图？element？ graph的样子
* 你到底解决什么问题？ reachable/ paths/ topological order/&#x20;
* dfs & bfs各个的细节



## DP

* 从dfs all paths 开始到 pure recursion
* 到dp，压缩空间&增加维度
* 别忘了bfs
