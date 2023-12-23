# Problem 3 Split Array Largest Sum





Step 1 dp definition

* dp\[k]\[i] represent the smallest largest sum we can get using first i element to parition into k pieces
* 用i个元素，分成k份，minimized largest sum是多少

Step 2 base case

* dp\[1]\[i] = sum of array\[j], j = 1, ...., i
* dp\[any]\[0] = XXX 没得可分，invalid case
* dp\[1]\[any] = 不用分，不用分就是所有元素= sum of elements!!&#x20;

Step3: Induction Rule

* dp\[k]\[i] = min of maximum in  (dp\[k - 1]\[j] (左大段) , sum\[array\[j+1], ... array\[i]])
  * \= minimum of all the way to parition, in each partition: maximum in (dp\[k - 1])\[j], prefixSum\[n] -prefixSum\[j])
  * 左大段，右小段
* length = j 左大段 | 右小段 index range: j to n-1



### 注意

注意那部分sum可以用prefix Sum

* \[0, arr\[0], arr\[0] + arr\[1],....., arr\[0] + arr\[1] ... arr\[j],..., arr\[0] + ...+ arr\[n - 1]]
* 0, 1, 2.....j,...,n

use case: sum of range \[j, n - 1]

* \[0, ... j - 1], \[0, ... n- 1] ===>. (j - 1, n-1]
* sum of range \[0, j - 1]: prefixSum\[j]
* sum of range\[0, n - 1]: prefixSum\[n]
* sum or range\[j, n - 1]: prefixSum\[n] - prefixSum\[j]
* 左大段的长度j也不是随意：
  * 不能切寂寞: j < 原始问题的长度 ==》 j <= n - 1
  * 为了让子问题还能分成k-1份，左大的段长度至少需要有长度k- 1
* valid range: \[k - 1， 愿问题的长度 - 1]

