# Problem 8 Classical Binary Search in 2D matrix



High Level:

* Search range index:  0, m\*n - 1
* need a map,&#x20;
  * row = index / column\_length
  * column = index % column\_length

```java
class Solution{
    public int[] search(int[][] matrix, int target) {
        int row_length = matrix.length;
        int col_length = matrix[0].length;
        int left = 0;
        int right = row_length * col_length -1;
        while (left <= right) {
            int mid = left + (right - left) /2;
            int mid_row = mid / col_length;
            int mid_col = mid % col_length;
            int candidate = mid[mid_row][mid_col];
            if (candidate == target) {
                return new int[]{mid_row, mid_col};
            } else if (candidate < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        
        }
        return new int[]{-1, -1};
    }

}
```
