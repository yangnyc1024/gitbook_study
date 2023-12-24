# Problem 3 Pizza



Step 1: DP定义

* dp\[i]\[j] represent the largest total sum of all pizza you can pick assuming you start first(from the ith pizza to the j tih pizza)

Step 2: Base case

* dp\[i]\[j] = array\[i]
* dp\[i]\[j] = array\[i] > array\[i+ 1]? array\[i]: array\[i+1]

Step 3: Induction Rule

* Case 1:我先从左边拿\[i+1, ...j]
  * 我朋友怎么拿？
    * 如果剩下左边的比右边打，我朋友拿左边第一个
    * 如果剩下左边的比右边的小，我朋友拿右边的第一个
* Case 2:  我从右边拿
  * 我朋友怎么拿？
    * 如果剩下右边的比左边大，我朋友拿右边的第一个
    * 如果剩下右边的比左边小，我朋友拿左边的第一个
