# Question 2 Search in Sorted Matrix



```java

/*
Clarification: 
  - sorted, integer, no repeated?
  - input: target(Integer), matrix(int[][]) 
  - output: int[]: row, col
Assumption:
High Level:
  - use binary search to find the target if it is in the matrix
Middle Level: using binary search to shrink the search range
  - find the value of mdx index,  
  - compare with it the given target 
  - decide which part you would like to go next
  - untile search range -> 0 or find the target?
TC&SC: O(logn), O(1)
*/


public class Solution {
  public int[] search(int[][] matrix, int target) {
    // Write your solution here

    // corner case
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
      return new int[]{-1, -1};
    }
    int totalRow = matrix.length;
    int totalCol = matrix[0].length;
    int left = 0;
    int right = totalRow * totalCol - 1;
    while (left <= right) {
      int midIndex = left + (right - left) / 2;
      int midRowIndex = midIndex / totalCol ;
      int midColIndex = midIndex % totalCol;
      int midValue = matrix[midRowIndex][midColIndex];
      if (midValue == target) {
        return new int[]{midRowIndex, midColIndex};
      }
      else if (midValue > target) {
        right = midIndex  - 1;
      }
      else {
        left = midIndex + 1;
      }
    }

    // 
    return new int[]{-1, -1};
  }
}
```
