# Graph Theory V: Shortest Path III Dijkstra Algorithm

## Series S2: 求一点出发到一点/其他所有点的最短路径

* 使用条件：边上的权证可以有且不相同但必须为正值
* Series S1:讲了五个series



### Part I: Dijkstra Algorithm基本过程与理解

**什么是Dijkstra Algorithm? Best First Search VS Dijkstra**

* Dijkstra：需要有一个Starting Node（题目给的），<mark style="color:purple;">每一次从到目前为止Cost最低的点出发（Expand）</mark>，generate所有它的邻居，直到我们Expand到targetNode/所有Node为止！
* <mark style="color:blue;">**每当一个点被Expand的时候，它的最短路径（从start到他）就确定了**</mark>

**Greedy算法**

* 不看所有解，我觉得按着某一种方法（aha point）去走，我就得到最优解
* Greedy算法需要证明，也需要一些灵感！

**反证法：会不会有一个被expand的点，其实从源点到它的最短路径没有确定，会在后面的expansion来确定**

* 被Generate的点， A(13), B(15), D(17)
* Expansion： dis(Src, first\_time\_C) = 10
* dis(Src, second\_expanded\_C) = initial dis from src to the cur node(>= 10) + dis of all the path behind
* dis(Src, second\_expanded\_C) > dis(Src, first\_time\_C)
* 假设错误

**在Dijsktra算法中需要注意**

* 明确你的cost是什么
* 我们允许一个点被Generate多次，先generate的不一定是最短路径（时间最先！=cost最优）
* 在有权重图中，<mark style="color:orange;">Mark Visited at Generation是不一定正确的！！</mark>

<mark style="color:blue;">**Cost of Neighbor When Generation**</mark>

* <mark style="color:blue;">dis(src, nei)  = dis(src, cur) + weight of (cur, nei)</mark>



**Use Case 1: 求出一个点到一个点的最短路径**



