# Question Extra Minimum cost to reach city with discounts



#### It is a graph

* city 点
* highway 边
* 这题是要求我们构建图中的带权重的最短路径问题，图是一个无向有环图
* 还有特殊限制，最多用discounts个打折卷可以把一条边上的权重削弱1/2

#### Method Dijkstra

* 点是什么？city是谁？到目前为止cost是多少？到目前为止用了多少张优惠卷？
* 怎么比较：
  * cost每一次走cost最小的点
* genenrate
  * case 1: 用优惠卷，到目前为止的还得有优惠劵可以用--》 mark visited checked
  * case 2: 不用优惠卷，原价generate --》mark visited

#### TC& SC

* O(Elog E)
* O(E)

#### 细节

* 以不同优惠卷数量的状态到大同一个city，这是一个解么？不是一个node
