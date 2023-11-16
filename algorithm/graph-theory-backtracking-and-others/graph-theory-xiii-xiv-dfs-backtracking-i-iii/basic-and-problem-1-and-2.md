# Basic & Problem 1&2



### Use case 1:所有解问题or all paths

所有解问题：all possible XXX--> 暴力解的根源



#### 明确backtracking问题里面，所谓的一个点允许多次是什么意思？

* alll path problem里，我们不允许同一个node在同一条path上使用多次，<mark style="color:blue;">但是我们允许同一个node在不同path上使用多次</mark>
* backtracking每个点有可能被访问多次，但within一条path里的每一个点最多访问一次
* DFS Mark Visited需不需要mark visited呢？<mark style="color:blue;">yes mark的是同一条路径上，这个点有没有被使用过</mark>

<mark style="color:blue;">**Discuss吃吐守恒，**</mark>**什么时候要吐呢？backtracking的时候，回溯的时候**

* 这条路径已经遍历完，准备回去尝试其他路径的时候



**Recursion，Pure Recursion，Backtrack，DFS这四个词什么关系？**

* pure recursion and dfs both implemented in reucrsion way, their difference is 构建解的顺序不一样
* pure recursion from bottom to top, dfs backtracking from top to bottom
* backtrack is the behavior of DFS：一定有从一个分支回去再访问另一个分支
