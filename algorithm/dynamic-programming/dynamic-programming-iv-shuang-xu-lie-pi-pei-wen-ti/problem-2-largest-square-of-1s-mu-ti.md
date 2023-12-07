# Problem Largest Square Of 1s





#### Method 1: Dynamic Programming

这是问题拓展longest consecutive 1 in array ==> largest square of 1s in Matrix



Step 1: dp 定义

* longest consecutive 1 in array:
  * includedp\[i] represents longest consecutive 1 ending at index I must include i
* largest square of 1s in matrix
  * dp\[i]\[j] represent largest square side length all 1 ending at i, j, must including i,j(特点：只有是1的点才需要更新，你都是不1，ending at你，没有全1的subarray，submatrix，square)
  * 问边长和问面积是一样的，肯定求的都是边长，面积 = 边长 \* 边长

Step 2: base case:

* longest consecutive 1 in array:
  * dp\[0] = array\[0]
* largest square of 1s in matrix
  * dp\[0]\[0] = matrix\[0]\[0]
  * 二维问题，第一行没有上方，第一列没有左边
  * dp\[0]\[any] = matrix\[0]\[any]
  * dp\[any]\[0] = matrix\[any]\[0]

Step 3: induction rule: linear scan 回头看

* longest consecutive 1 in array:
  * &#x20;dp\[i] = array\[i] == 1? dp\[i-1] + 1: 0
* largest square of 1s in Matrix:
  * dp\[i]\[j] = matrix\[i]\[j] == 1? math.min(dp\[i]\[j - 1], dp\[i -1]\[j ], d\[\[i -1]\[j -1]) + 1 : 0

Step 4: 填写方式

* 从上到下，从左到右
