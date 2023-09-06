# Question 11 Valid Paretheses II



计算还没有闭合的括号一共有多少个？

* 每次遇到\*，max++；min = Math.max(0, min -1);
* 出现false就是max小的
