# Question 1 Island 母体二刷

### 解题步骤

#### Step 1: State the problem归大类

* Actually, this is a Graph Problem
* I want to model the problem to a Graph problem.

#### Step 2: Build Graph

* Let me build the graph.
* In my graph
  * my node/ vertex is every "1" cell in the matrix
  * edge: horizontally or vertically each one is connected with four directions with its neightbors

#### Step 3: 转化问题

* 脱马甲，这个问题其实本质上就是在解决你构建的哪个图上的什么问题
* 问一下面试官：OK, do you quite follow? Do you have any questions about the graph I built?
* So the problem is asking me to find out the number of islands, which is actually asking me how many <mark style="color:blue;">connected components</mark> are there in the graph I built

#### Step 4:这个问题在图论里面是个什么问题

* Therefore this is a traversal(reachable) problem in graph

#### Step 5: Propose 算法对比，选择最优

* DFS对点的遍历
* BFS对点的遍历
* 对比：时间空间复杂度，商讨具体实现的细节，选择一个最好的来写



### Method 1: DFS对点的遍历





### Method 2: BFS对点的遍历
