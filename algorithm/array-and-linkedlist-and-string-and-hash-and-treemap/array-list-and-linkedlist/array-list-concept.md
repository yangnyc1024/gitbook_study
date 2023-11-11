# Array/ List

## What is Array/ List?



#### How to create a list in java? how about matrix?

* Array代表的是class
  * 一般不直接去用它，不会这样写 new Array()， 只会，int\[] array = new int\[3].
* array的length是final variable

```java
// method 1
int[] array = new int[array.length]
ElementType[] arrayName = new ElementType[arrray dot length]
// method 2
int[] array = new int[]{}


int[][] matrix = new int[length_of_row][length_of_col]
ElementType[][] matrixName = new ElementType[第一维度][第二维度]

```

* 小array就是逻辑上的数组，
* Arrays是java里的类，是utility 类型，你用了可以快速操作
  * 这些是static的method，无需要new一下

**二维array在内存上发生什么事情？**

* 高维数组，是指向低维数组的reference的数组





