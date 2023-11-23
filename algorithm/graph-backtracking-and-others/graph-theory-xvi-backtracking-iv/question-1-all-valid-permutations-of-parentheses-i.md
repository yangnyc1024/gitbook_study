# Question 1: All Valid Permutations Of Parentheses I

* Question 0:  这个是N=2的所有可能解吗？if all, should be 6?
* pre question: 给你一个String of括号
* 合法性问题Valid：左右需要match不能有open的左或者右

合法性验证：

* 遇到左括号leftAddedSoFar++
* 遇到右括号rightAddedSoFar++
* 任意时刻leftAddedSoFar < rightAddedSoFar
* 结束的时候还要小心 左open也必须等于0



## Follow Up:&#x20;

```java
```
