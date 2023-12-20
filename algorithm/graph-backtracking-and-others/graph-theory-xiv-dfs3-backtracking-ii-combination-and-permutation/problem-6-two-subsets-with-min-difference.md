# Problem 6 Two Subsets With Min Difference

#### Following Up question

Question: Given a set of n integers, divide the set into two subsets of n/2 size each such that the difference of the sum of two subsets is as minimum as possible. Return the minium difference(absolute value)

脱马甲的方式：把你构建的解的方式说出来：以加为不加：要么XXXX，要么XXXX

High Level + Recursion Tree:把每个元素分到两个subset里去，对于每个元素来说，要么去A，要么去B

tips

* 如果你知道total Sum，只记录A的Sum：BSum = totalSum - ASum
* Math.abs(total - Asum) - Asum) represent 两个subset. sum的差



```java
// Some code

public int mindifference(int[] array) {
    int[] min = new int[]{Integer.MAX_VALUE};
    DFS(array, 0, 0 , 0 , min, 0);
    return min[0];
}
// ASum: sum of subset A
// BSum: sum of subset B
// index: which index is considered in current level
// countA: subset A's size
private void DFS(int[] array, int ASum, int BSum, int index, int[] min, int countA) {
    if (index == array.length) {
        if (countA == array.length / 2) {
            min[0] = Math.min(min[0], Math.abs(ASum - BSum));
        }
        return;// 只要到Base case 必须终止程序，不然下面就超界了
    }
    // 如果你A里的size已经超过了n/2+ 1
    if (countA > array.length / 2 + 1) {
        return;
    }
    // 要不进A
    DFS(array, ASum + array[index], BSum, index + 1, min, countA + 1);
    // 要不进B
    DFS(array, ASum , BSum + array[index], index + 1, min, countA);
}
```
