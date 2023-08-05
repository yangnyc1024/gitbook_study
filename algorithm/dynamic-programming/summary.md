# Summary

DP的问题其实常常伴随着五种方法：

#### BFS

* bfs相当于你每一层在压缩信息，用greedy的方式来储存，用local optimal 直到找到global path

#### dfs all paths

* dfs all paths相当于你用horse hails的角度把每一个path都找出来

#### dfs pure recursion

* dfs pure recursion: tails recursion?
  * back的all path？但是又储存所有

#### dfs memo

* dfs memo------基本上只作用在DAG上
  * 相当于把你对应的cost储存

#### dp

* dp-----基本上只作用在DAG
  * back 的iteration的方式？
* 好处是可以填表的时候压缩空间？





Question：其他和DAG的关系呢？
