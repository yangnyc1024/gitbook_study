# Tree with Pure Recursion and Backtracking

Pure Recursion: 该点作为root，从后面问题继承的，如何给回之前以至于找到解

* curResult.left(), <mark style="color:red;">after curPoint</mark>
* curResult.right(), <mark style="color:red;">after curPoint</mark>
* 小心你的base case， cur == null  , AND, cur.left == null & cur.right == null
* 小心你的cur.left or cur.right 小心cur有没有，cur.left & cur.right 有么有

Backtracking: 该点作为ending point, 如何利用之前继承的，往下找到解

* f(curPoint, resultInfor<mark style="color:red;">Before</mark>CurPoint, curResultInfor<mark style="color:red;">Before</mark>CurPoint)





