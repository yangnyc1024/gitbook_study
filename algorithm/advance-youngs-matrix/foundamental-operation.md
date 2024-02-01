# Foundamental operation

#### Q1 Search for a target value in the Young Matrix

Solution 1: Brute Force



Solution 2: Binary Search

for each row:进行bainary search

1.1 each row is sorted --> binary search on each of the rows O(nlogm)

1.2 each col is sorted --> binary search on each of the cols O(mlogn)





Solution 3: BST view

O(m+ n)



```java
public boolean find(int[][] matrix, int target) {
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
         return false;
    }
    int i = 0;
    int j = matrix[0].length - 1;
    while (j > 0 && i < matrix.length){
         if (matrix[i][j] == target) return true;
         if (matrix[i][j] < target) {
              i++;
         }
         else {
              j--;
         }
    }
    return false;
}
```



哪一个好？
