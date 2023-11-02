# Question 8 Graph coneectivity With Threshold

如果入手点事Union Find

* 思考方向就是，我怎么知道两个人可以union？union的事什么

Cities with labels x and y have a road between them if there exists an interger z such taht all of the following are true:

* x % z== 0
* y % z== 0
* z > threshold

拆分Query(x, y)和union（x和z的倍数）：<mark style="color:blue;">z的共同好友</mark>

* x和y如果能union的话，x和constant \* z是同一组的人么？
* x和2z，x和3z。。。for all z from \[threshold + 1, n]其实都是同一组
* y和2z，y和3z。。。for all z from \[threshold + 1, n]其实都是同一组
