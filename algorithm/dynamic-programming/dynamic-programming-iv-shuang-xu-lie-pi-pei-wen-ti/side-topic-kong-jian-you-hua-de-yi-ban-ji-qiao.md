# Side Topic: 空间优化的一般技巧

#### 情况1:一条线： 一维dp array

case1: dp\[i] only depends on dp\[i-1] --> O(1)的空间就可以

case2: dp\[i] not only depends on dp\[i-1]



#### 情况2:一个面：二维dp matrix

假如我们的情况是从左到右，从上到下更新的过程

* 结论1:两行肯定没问题，我们一定不需要多于两行
* 优化方法1:用mod符号
  * example
  * dp\[i]\[j] = dp\[i -1]\[j - 1] + dp\[i-1]\[j] + dp\[i]\[j - 1]
  * dp\[i % 2]\[j] = dp\[(i -1) % 2]\[j - 1] + dp\[(i-1) % 2]\[j] + dp\[i % 2]\[j - 1]
  * 优点：比较快速的可以写出来，缺点没有做到最优，可能可以更经济 O(n^2) -> O(n)
* 优化方法2:一行可不可以呢？
  * 直接写遇到的问题，dp\[i - 1]\[j - 1]这个值，其实已经被我在更新dp\[i]\[j - 1]的时候给抹掉了，现在就没法更新dp\[i]\[j]了
  * 我现在正在填写dp\[i-1]\[j], 我正在抹掉dp\[i -1]\[j], 现在正在抹掉的值，就是我下一次更新dp\[i]\[j+1]的时候，所需要的左上角
  * 那我就记下来
    * int\[] dp <- new int\[column length]
    * base case here:
      * 从上倒下更新，For i from 0 to last row:
        * int已经抹掉的左上角 = 0；
        *   从左到右更新：for j from 0 to last col:

            // we need to fill in dp\[j] here

            * int 即将要抹掉正上方 = dp\[j]
            * dp\[j] updated by (即将要抹掉的正上方，已经抹掉的左上角, dp\[j -1])
            * 已经抹掉的左上角 = 即将要抹掉的正上方

