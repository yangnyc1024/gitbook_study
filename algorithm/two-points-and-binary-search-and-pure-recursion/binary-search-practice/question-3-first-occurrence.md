# Question 3 First Occurrence

```java
/*
Clarification & Assumption
  - Input: int[] array, int target
  - Output: return the index

High Level
  - applying binary search to shrink down the search range until we find
Middle Level
  - each time, find the mid point and compare array[mid_point] vs target

TC &SC: O(log N), O(1)
*/

public class Solution {
  public int firstOccur(int[] array, int target) {
    // Write your solution here

    // corner case
    if (array == null || array.length == 0) {
      return -1;
    }

    // find midpoint
    int left = 0;
    int right = array.length - 1;
    while (left < right - 1) {
      int mid = left + (right - left) / 2;
      if (array[mid] == target) {
        right = mid;
      }
      else if (array[mid] > target) {
        right = mid - 1;
      }
      else {
        left = mid;
      }

    }
    if (array[left] == target) {
        return left;
    }
    if (array[right] == target) {
      return right;
    }
    return -1;
  }
}
```
