# Summary

## 在什么样的图上

### Graph的表达

* <mark style="color:red;background-color:red;">**Vertex（说白了就是你需要所有关于你traverse的信息**</mark><mark style="color:red;">**）**</mark>
  * <mark style="color:blue;">**重要信息1和别人的关系**</mark>——Edge: neighbors
    * edge很重要一方面是标识你周围有几个vertex
    * 还有就是怎么样的花费到这些点——weight
    * 常用data structure见后面
  * <mark style="color:blue;">**重要信息2自己的info**</mark>——Visited
    * 常用data structure见后面
  * <mark style="color:blue;">**重要信息2自己的info**</mark>——Value/Weight？
  * <mark style="color:blue;">**重要信息2自己的info**</mark>——Position (x, y)
    * 位置如果自定义的data structure注意是否要重写hashcode& equal\

* Visited& Visiting
  * set\_visited
  * map of \<Vertex, Enum\_State>
* Indegree
  * map of \<Vertex, Indegree>
* graph的表达式 Vertex\&Edge&#x20;
  * int\[]\[]
  * Map\<Vertex, Set/List\<Integer>>
  * Vertex {int, List<>neighbors}——<mark style="color:red;">这个是首选！！！</mark>\


## 解决一个什么样的问题

* tree？
  * indegree 全部为1
  * |V|  = |E| + 1\

* DAG
  * topological order？cycle？这两个是一样的？
  * dfs visiting?
  * bfs indegree?
* general
  * Reachable?
  * path?
    * shortest path ---- 注意any？all？one ？ to  any？all？one ？

## 用什么样的遍历问题（注意最原始的遍历问题都是从一个点开始）

### DFS1

1）从一个给定的点，2）traverse all reachable nodes，3）通过深度优先的准则，4）保证每个点都visited一次

### DFS2&#x20;

从一个给定的点，traverse all reachable nodes，通过深度优先的准则，保证每个点都visited一次（在第一次visited时候<mark style="color:purple;">mark visiting</mark>，在它的neighbor visiting完了以后<mark style="color:purple;">mark visited</mark>），主要负责解决有环无环/有没有dependence

* 注意dfs常在generate的时候就check visited

### DFS3

从一个给定的点，去找all possible path，通过深度优先的准则（在第一次visited时候mark visited，在它的neighbor visited完了以后mark unvisited）

* check condition:
  * visited? boundary check? reachable check?
  * change state
  * 注意你在哪里标visited的问题

### BFS1

It starts at the initial point and explores all nodes at the present depth prior to moving on to the nodes at the next depth level. <mark style="color:red;">(by level order???)</mark>

initial queue

* 判断nei符合条件
* 判断nei是否可以visited（visited? boundary check? reachable check?）
* visited and offer together!!!

BFS algorithm框架

* size
* generate
* expand
  * 生成nei
  * 判断nei符合条件
  * 判断nei是否可以visited（visited? boundary check? reachable check?）
    * visited and offer together!!!



### BFS2

* 需要注意在expand和gen的时候的不同

\
\
\


### DFS + backtracking

#### 思考方式

* high level怎样一步一步来构造一个解
  * 小心有序？
  * 小心重复？
* middle level
  * 你的函数是什么？
  * recursive rule
* branch是什么？在每个branch
  * level是是什么？
  * base case / add result（重点是你怎么结束）
* TC\&SC

#### 需要注意的地方

* all permutation//all subsets&#x20;
  * 目前我们主流的做法，只有一个一个（一群一群的）放的做法（因为你有顺序，当然可以当作没有顺序）
  * all subsets还多出一种，就是一种一种类型放
* 要十分小心base case的前后问题&所有对于该问题多加的限制条件（ex：size = k, 一共有几个）
* 如果有重复value，你可以把他们group起来一起处理
* 你的吐与不吐，不代表一定是在for loop外面？（dfs3 in graph是这样），但是不是完全这样子





缺高阶的图的问题
